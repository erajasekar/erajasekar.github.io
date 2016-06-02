---
layout: post
title: Error accumulation in validation using Applicative Functors
date: 2016-05-31
draft: false
tags: java8 java functional programming monad functor
comments: true
description: This post explains how Applicative Functors can be used accumulate validation errors using Javaslang's Validation API.
analytics: true
---

This post explains how ***Applicative Functors*** can be used accumulate validation errors using [Javaslang](http://www.javaslang.io/) validation API.

## Problem

To illustrate with an example, let's say a given stream of pair of date strings in format `MM/dd/YYYY`, we want to print difference between them in number of years, months and days. ( For eg `"01/01/2016 , 02/01/2016"` should print `0 years , 1 months and 0 days`). 
<br>

### Using plain Java 8.

Let's try first try to solve this in plain Java without functional programming library. As I have explained in the [previous post]({% post_url 2016-05-27-better-exception-handling-java8-streams-using-javaslang %}), we should use `Optional` to ensure it continues to process *without terminating at the first error*. Here how we can implement it.

```java

public class ValidationWithErrorAccumulation {

    private static final DateTimeFormatter formatter = DateTimeFormatter.ofPattern("MM/dd/yyyy");

    /**
     * Parses given dates string in format "MM/dd/yyyy" to LocalDate and converts it to Period
     * Returns Optional of Period if it is valid, otherwise Optional.empty
     */
   private static Optional<Period> parseDateToPeriod(String dateString1, String dateString2){
        LocalDate date1 = null , date2 = null;
        try {
            date1 = LocalDate.from(formatter.parse(dateString1));
            date2 = LocalDate.from(formatter.parse(dateString2));
        }catch (DateTimeParseException e){
            System.out.println(e.getMessage());
        }
        return date1 != null && date2 != null ?
                Optional.of(Period.between(date1, date2)) :
                Optional.empty();
    }

    /**
     * Formats given Period as String representing number of years, months and days.
     */
    private static String toRelative(Period p){
        return String.format("%s years , %s months and %s days", p.getYears(), p.getMonths(), p.getDays());
    }

    public static void main(String args[]) {
        Stream.of("01/01/2015 , 12/31/2015",
                "01-01-2015 , 12-31-2015",
                "01/12/2014 , 01/01/2015",
                "01/01/2016 , 02/01/2016")
                .map(s -> s.split(" , ")) //Split pair of dates
                .map(v -> parseDateToPeriod(v[0],v[1])) //Parse them to Period
                .filter(Optional::isPresent) //Filter valids
                .map(Optional::get) //Get wrapped value
                .map(ValidationWithErrorAccumulation::toRelative) //Format to Relative String containing # of years, months, days
                .forEach(System.out::println);//Print
    }
}

```

This will output

```sh
0 years , 11 months and 30 days
Text '01-01-2015' could not be parsed at index 2
0 years , 11 months and 20 days
0 years , 1 months and 0 days
```

This works and processes all the valid dates, but this solution has several limitations.

+ The validation stops at first error when the start date is invalid, we will get to know that end date is also invalid only after correcting the first date and retrying. It is useful to accumulate all errors so that all can be fixed at once.
Especially, when doing validation of multiple fields, say a web form, and you want to know all errors encountered, instead of one at a time.
+ The validation error has to be handled within `parseDateToPeriod` as `Optional` can only hold valid values and not errors from invalids.


### Using Validation API in Javaslang

Above limitations can be solved using [Javaslang](http://www.javaslang.io/) functional library. It facilitates accumulating errors using *applicative functor* [validation](http://www.javaslang.io/javaslang-docs/#_validation) control. In addition, we can leverage [Tuples](http://www.javaslang.io/javaslang-docs/#_tuples) to get rid of clumsy splitting of date strings with comma.  

```java
public class ValidationWithErrorAccumulation {

    private static final DateTimeFormatter formatter = DateTimeFormatter.ofPattern("MM/dd/yyyy");
    
    /**
     * Parses given tuple of two dates to Period and accumulates errors. 
     * Returns Validation of Period if both dates are valid, otherwise Validation of list of error messages.
     */
    private static Validation<List<String>, Period> parseDateToPeriod(Tuple2<String,String> dates){
        return  parseDate(dates._1()).combine(parseDate(dates._2())).ap( (date1, date2) -> Period.between(date1,date2));
    }

    /**
     * Parses given date string in format "MM/dd/yyyy" to LocalDate
     * Returns Validation of LocalDate if it is valid, otherwise Validation of String containing error message.
     */
    private static Validation<String,LocalDate> parseDate(String dateString){
        Try<LocalDate> parsedDate = Try.of(() -> LocalDate.from(formatter.parse(dateString)));
        return parsedDate.isSuccess() ? Validation.valid(parsedDate.get()) : Validation.invalid(parsedDate.getCause().getMessage());
    }

    /**
     * Formats given Period as String representing number of years, months and days.
     */
    private static String toRelative(Period p){
        return String.format("%s years , %s months and %s days", p.getYears(), p.getMonths(), p.getDays());
    }
    
    public static void main(String args[]) {
        Stream.of(Tuple.of("01/01/2015","12/31/2015"),
                Tuple.of("01-01-2015","12-31-2015"),
                Tuple.of("01/12/2014","01/01/2015"),
                Tuple.of("01/01/2015","01/01/2016"))
                .map(ValidationWithErrorAccumulation::parseDateToPeriod) //Parse dates to Period
                .peek(v -> {
                    if (v.isInvalid())
                        System.out.println(v.getError());
                })//Print errors for invalid ones
                .filter(Validation::isValid) //Filter valids
                .map(Validation::get) //Get wrapped Period
                .map(ValidationWithErrorAccumulation::toRelative) //Format to Relative String containing # of years, months, days
                .forEach(System.out::println);//Print
    }
}
```

Here is the output that shows errors for both start and end dates.

```sh
0 years , 11 months and 30 days
List(Text '01-01-2015' could not be parsed at index 2, Text '12-31-2015' could not be parsed at index 2)
0 years , 11 months and 20 days
1 years , 0 months and 0 days
```

#### Choosing between Try Monad and Validation Applicative Functor

In the [previous post]({% post_url 2016-05-27-better-exception-handling-java8-streams-using-javaslang %}) , I illustrated using *Try monad* to gracefully deal with failures. When trying to compose with Monads, the combination process will short circuit at the first encountered error. But *Validation applicative functor* will continue processing the combining functions, accumulating all errors. So we should use **Try** for *fail fast* and **Validation** for *fail slow* scenarios.

