---
layout: post
title: Better Exception Handling in Java 8 Streams Using Javaslang
date: 2016-05-27
draft: false
tags: java8 java functional programming monad
comments: true
description: In this post I will provide tips for better exception handling in Java 8 streams using Javaslang Functional Java library.
analytics: true
---

In this post, I will provide tips for better exception handling in Java 8 streams using Functional Java library [Javaslang](http://www.javaslang.io/).

## Problem

To illustrate with an example, let's say we want to print day of the week for given stream date strings in format `MM/dd/YYYY`.
<br>

### Initial solution.

Let's start with an initial solution below and iteratively improve on it.

```java

public class StreamExceptionHandling {

    private static final DateTimeFormatter formatter = DateTimeFormatter.ofPattern("MM/dd/yyyy");

    /**
     * Converts given date string in format "MM/dd/yyyy" to LocalDate.
     */
    private static LocalDate parseDate(String dateString) {
        return LocalDate.from(formatter.parse(dateString));
    }
    public static void main(String args[]) {
        Stream.of("12/31/2014",
                "01-01-2015",
                "12/31/2015",
                "not a date",
                "01/01/2016")
                .map(StreamExceptionHandling::parseDate) //parse string to LocalDate
                .map(DayOfWeek::from) // Map LocalDate to Day of Week
                .forEach(System.out::println); // Print
    }
}

```

This will output

```sh
WEDNESDAY
Exception in thread "main" java.time.format.DateTimeParseException: Text '01-01-2015' could not be parsed at index 2
...
```

*Huh*, If a date string is invalid, this fails at the first *DateTimeParseException* without continuing with valid dates.

### Java 8 Optional to rescue.

We can refactor `parseDate` to return `Optional<LocalDate>` to make it discard invalids and continue processing valid dates.

```java

/**
 * Converts given date string in format "MM/dd/yyyy" to LocalDate.
 * Returns Optional of LocalDate if it is valid, otherwise Optional.empty
 */
private static Optional<LocalDate> parseDate(String dateString){
    LocalDate localDate = null;
    try {
        localDate = LocalDate.from(formatter.parse(dateString));
    }catch (DateTimeParseException e){
        System.out.println(e.getMessage());
    }
    return Optional.ofNullable(localDate);
}

public static void main(String args[]) {
    Stream.of("12/31/2014",
            "01-01-2015",
            "12/31/2015",
            "not a date",
            "01/01/2016")
            .map(StreamExceptionHandling::parseDate)//Parse String to LocalDate
            .filter(Optional::isPresent) //Filter valid ones
            .map(Optional::get)//Get wrapped LocalDate
            .map(DayOfWeek::from) //Map to day of week
            .forEach(System.out::println); //Print
}

```

This will skip errors and converts all the valid dates.

```sh
WEDNESDAY
Text '01-01-2015' could not be parsed at index 2
THURSDAY
Text 'not a date' could not be parsed at index 0
FRIDAY
```

This is great improvement, but the exception has to be handled within `parseDate` method and can't be passed back to main method to deal with it. We can't make `parseDate` method throw checked exception as Streams API doesn't play well with methods that throw exceptions.

### Better solution with Javaslang's Try Monad

[Javaslang](http://www.javaslang.io/) is a functional library for Java 8+. We will use `Try` object from Javaslang which can be either a instance of `Success` or `Failure`. Basically [Try](http://www.javaslang.io/javaslang-docs/#_try) is a monadic container type which represents a computation that may either result in an exception, or return a successfully computed value. Here is the modified code using *Try*

```java

/**
 * Converts given date string in format "MM/dd/yyyy" to LocalDate.
 * Returns Try of LocalDate representing valid LocalDate or Throwable in case of invalid value.
 */
private static Try<LocalDate> parseDate(String dateString){
    return Try.of(() -> LocalDate.from(formatter.parse(dateString)));
}

public static void main(String args[]) {
    Stream.of("12/31/2014",
            "01-01-2015",
            "12/31/2015",
            "not a date",
            "01/01/2016")
            .map(StreamExceptionHandling::parseDate)//Parse String to LocalDate
            .peek(v-> v.onFailure(t -> System.out.println("Failed due to " + t.getMessage())))//Print error on failure
            .filter(Try::isSuccess)//Filter valids
            .map(Try::get)//Get wrapped value
            .map(DayOfWeek::from)//Map to day of week
            .forEach(System.out::println);//Print
}

```

The Output is

```sh

WEDNESDAY
Failed due to Text '01-01-2015' could not be parsed at index 2
THURSDAY
Failed due to Text 'not a date' could not be parsed at index 0
FRIDAY
```

Now the exception is passed back to main to deal with it. Try also has API's to implement a recovery logic or return default value in case of error. To demonstrate this, let's say we also want to support `MM-dd-YYYY` as alternate string format for date. Below example shows how we can easily implement recovery logic.

```java

public class StreamExceptionHandling {

    private static final DateTimeFormatter formatter = DateTimeFormatter.ofPattern("MM/dd/yyyy");
    private static final DateTimeFormatter alternateFormatter = DateTimeFormatter.ofPattern("MM-dd-yyyy");

    /**
     * Converts given date string in format "MM/dd/yyyy" to LocalDate.
     * Returns Try of LocalDate representing valid LocalDate or Throwable in case of invalid value.
     */
    private static Try<LocalDate> parseDate(String dateString){
        return Try.of(() -> LocalDate.from(formatter.parse(dateString)));
    }

    /**
     * Converts given date string in format "MM/dd/yyyy" to LocalDate.
     * Returns Try of LocalDate representing valid LocalDate or Throwable in case of invalid value.
     */
    private static Try<LocalDate> parseDateAlternate(String dateString){
        return Try.of(() -> LocalDate.from(alternateFormatter.parse(dateString)));
    }

    public static void main(String args[]) {
        Stream.of("12/31/2014",
                "01-01-2015",
                "12/31/2015",
                "not a date",
                "01/01/2016")
                .map(StreamExceptionHandling::parseDate)//Parse String to LocalDate
                .map(v-> v.recoverWith( e -> parseDateAlternate(((DateTimeParseException)e).getParsedString())))//Try recovering with alternate formatter
                .peek(v-> v.onFailure(t -> System.out.println("Failed due to " + t.getMessage())))//Print error on failure
                .filter(Try::isSuccess)//Filter valids
                .map(Try::get)//Get wrapped value
                .map(DayOfWeek::from)//Map to day of week
                .forEach(System.out::println);//Print
    }
}
```

The output shows that now the date `01-01-2015` is also successfully converted.

```sh
WEDNESDAY
THURSDAY
THURSDAY
Failed due to Text 'not a date' could not be parsed at index 0
FRIDAY
```

So *Try Monad* can be used to elegantly deal with exceptions and *fail fast* on errors. In [next article]({% post_url 2016-05-31-error-accumulation-java8-functional-validation-javaslang %}) , I will post how *Validation control applicative functor* can be used to *fail slow* and accumulate errors. 
