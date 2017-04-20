Java 8 examples to show you how to convert from `Instant` to `ZonedDateTime`

## 1\. Instant -> ZonedDateTime

Example to convert a `Instant` UTC+0 to a Japan `ZonedDateTime` UTC+9

InstantZonedDateTime1.java

    package com.mkyong.date;

    import java.time.Instant;
    import java.time.ZoneId;
    import java.time.ZonedDateTime;

    public class InstantZonedDateTime1 {

        public static void main(String[] argv) {

            // Z = UTC+0
            Instant instant = Instant.now();

            System.out.println("Instant : " + instant);

            // Japan = UTC+9
            ZonedDateTime jpTime = instant.atZone(ZoneId.of("Asia/Tokyo"));

            System.out.println("ZonedDateTime : " + jpTime);

            System.out.println("OffSet : " + jpTime.getOffset());

        }

    }

Output

    Instant : 2016-08-18T06:17:10.225Z
    LocalDateTime : 2016-08-18T06:17:10.225

## 2\. ZonedDateTime -> Instant

Convert the Japan `ZonedDateTime` UTC+9 back to a `Instant` UTC+0/Z, review the result, the offset is taken care automatically.

InstantZonedDateTime2.java

    package com.mkyong.date;

    import java.time.*;

    public class InstantZonedDateTime2 {

        public static void main(String[] argv) {

            LocalDateTime dateTime = LocalDateTime.of(2016, Month.AUGUST, 18, 6, 57, 38);

            // UTC+9
            ZonedDateTime jpTime = dateTime.atZone(ZoneId.of("Asia/Tokyo"));

            System.out.println("ZonedDateTime : " + jpTime);

            // Convert to instant UTC+0/Z , java.time helps to reduce 9 hours
            Instant instant = jpTime.toInstant();

            System.out.println("Instant : " + instant);

        }

    }

Output

    ZonedDateTime : 2016-08-18T06:57:38+09:00[Asia/Tokyo]
    Instant : 2016-08-17T21:57:38Z

## References

1.  [Wikipedia – ISO 8601 date format](https://en.wikipedia.org/wiki/ISO_8601)
2.  [Instant JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html)
3.  [ZoneddateTime JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/ZonedDateTime.html)

[http://www.mkyong.com/java8/java-8-convert-instant-to-zoneddatetime/](http://www.mkyong.com/java8/java-8-convert-instant-to-zoneddatetime/)
