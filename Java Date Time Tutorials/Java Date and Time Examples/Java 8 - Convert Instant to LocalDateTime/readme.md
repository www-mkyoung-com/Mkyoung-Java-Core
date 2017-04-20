Java 8 examples to show you how to convert from `Instant` to `LocalDateTime`

## 1\. Instant -> LocalDateTime

The `java.time.LocalDateTime` has no concept of time zone, just provide a zero offset UTC+0.

InstantExample1.java

    package com.mkyong.date;

    import java.time.Instant;
    import java.time.LocalDateTime;
    import java.time.ZoneOffset;

    public class InstantExample1 {

        public static void main(String[] argv) {

    		// Parse a ISO 8601 Date directly
    		//Instant instant = Instant.parse("2016-08-18T06:17:10.225Z");

            Instant instant = Instant.now();

            System.out.println("Instant : " + instant);

            //Convert instant to LocalDateTime, no timezone, add a zero offset / UTC+0
            LocalDateTime ldt = LocalDateTime.ofInstant(instant, ZoneOffset.UTC);

            System.out.println("LocalDateTime : " + ldt);

        }

    }

Output

    Instant : 2016-08-18T06:17:10.225Z
    LocalDateTime : 2016-08-18T06:17:10.225

## 2\. LocalDateTime -> Instant

InstantExample2.java

    package com.mkyong.date;

    import java.time.*;

    public class InstantExample2 {

        public static void main(String[] argv) {

    		// Hard code a date time
            LocalDateTime dateTime = LocalDateTime.of(2016, Month.AUGUST, 18, 6, 17, 10);

            System.out.println("LocalDateTime : " + dateTime);

            // Convert LocalDateTime to Instant, UTC+0
            Instant instant = dateTime.toInstant(ZoneOffset.UTC);

            System.out.println("Instant : " + instant);

        }

    }

Output

    Instant : 2016-08-18T06:17:10.225Z
    LocalDateTime : 2016-08-18T06:17:10.225

## References

1.  [Wikipedia – ISO 8601 date format](https://en.wikipedia.org/wiki/ISO_8601)
2.  [Instant JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html)
3.  [LocaldateTime JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html)

[http://www.mkyong.com/java8/java-convert-instant-to-localdatetime/](http://www.mkyong.com/java8/java-convert-instant-to-localdatetime/)
