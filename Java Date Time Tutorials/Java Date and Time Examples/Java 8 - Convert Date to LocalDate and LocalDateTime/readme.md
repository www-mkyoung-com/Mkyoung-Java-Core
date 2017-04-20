The `java.util.Date` has no concept of time zone, and only represents the number of seconds passed since the [Unix epoch time](https://en.wikipedia.org/wiki/Unix_time) – 1970-01-01T00:00:00Z (midnight at the start of January 1, 1970 GMT/UTC)

**Note**  
The new Java 8 `java.time.Instant` is the equivalent class to the classic `java.util.Date`

## 1\. Date -> java.time

The idea for the date conversion :

<pre>Date -> Instant + System default time zone = LocalDate
Date -> Instant + System default time zone = LocalDateTime
Date -> Instant + System default time zone = ZonedDateTime
</pre>

This example shows you how to convert `java.util.Date` to the new Java 8 Date APIs – `LocalDate`, `LocalDateTime` and `ZonedDateTime`

DateToJavaTime.java

    package com.mkyong.java8;

    import java.time.*;
    import java.util.Date;

    public class DateToJavaTime {

        public static void main(String[] args) {

            //Asia/Kuala_Lumpur +8
            ZoneId defaultZoneId = ZoneId.systemDefault();
            System.out.println("System Default TimeZone : " + defaultZoneId);

            //toString() append +8 automatically.
            Date date = new Date();
            System.out.println("date : " + date);

            //1\. Convert Date -> Instant
            Instant instant = date.toInstant();
            System.out.println("instant : " + instant); //Zone : UTC+0

            //2\. Instant + system default time zone + toLocalDate() = LocalDate
            LocalDate localDate = instant.atZone(defaultZoneId).toLocalDate();
            System.out.println("localDate : " + localDate);

            //3\. Instant + system default time zone + toLocalDateTime() = LocalDateTime
            LocalDateTime localDateTime = instant.atZone(defaultZoneId).toLocalDateTime();
            System.out.println("localDateTime : " + localDateTime);

            //4\. Instant + system default time zone = ZonedDateTime
            ZonedDateTime zonedDateTime = instant.atZone(defaultZoneId);
            System.out.println("zonedDateTime : " + zonedDateTime);

        }

    }

Output

<pre>System Default TimeZone : Asia/Kuala_Lumpur

date : Fri Aug 19 21:46:31 MYT 2016
instant : 2016-08-19T13:46:31.981Z

localDate : 2016-08-19
localDateTime : 2016-08-19T21:46:31.981
zonedDateTime : 2016-08-19T21:46:31.981+08:00[Asia/Kuala_Lumpur]
</pre>

## 2\. Explanation – Q&A

**2.1 Question** : If `Date` has no concept of time zone, why the time zone will be displayed while we print out the `Date` object? For example :

    //Fri Aug 19 11:52:06 MYT 2016
    System.out.println(new Date()); //MYT = my system default time zone

**Answer** : Check the `java.uti.Date.toString()` source code, if you print out the `Date` object, the system default time zone will be appended and display together.

java.util.Date

    public String toString() {

            //...omitted...

            TimeZone zi = date.getZone();
            if (zi != null) {
                sb.append(zi.getDisplayName(date.isDaylightTime(), TimeZone.SHORT, Locale.US)); // zzz
            } else {
                sb.append("GMT");
            }
            sb.append(' ').append(date.getYear());  // yyyy
            return sb.toString();
    }

**Note**  
This behavior is a design flaw since JDK1.1, it makes a lot of confusion. Again, the `java.util.Date` doesn’t store any time zone info, but if you print it out, the system default time zone will be displayed together.

**2.2 Question **: For the `Date` conversion, why we need to add a system default time zone for `java.time.instant`?  
**Answer** : Refer to the above 2.1 Q&A. Review another example :

<pre>1\. Date = 19/08/2016T10:00:00
2\. System default time zone = +08:00 [Asia/Kuala_Lumpur]
3\. Date (Print) = 19/08/2016T10:00:00+08:00 = 19/08/2016T18:00:00
</pre>

The goal of the conversion is make sure both print `Date` and print `LocalDate` will generates the same output.

<pre>// Assume 19/08/2016T10:00:00 = 1000
// System default time zone = +8

1\. Date (1000) -> Print Date (1000) = 1000+08:00  
// we always see "1000+08:00" (but the Date is still 1000)

2\. Date (1000) -> Instant (1000)
// instant has no time zone or zero offset (UTC+0/Z)

3\. Instant(1000) -> LocalDate(1000) -> Print LocalDate(1000) = 1000
// The result is "1000", different with print date!

4\. LocalDate(1000) + 08:00 -> LocalDate(1000+08:00)
// add default time zone +8

5\. Print LocalDate(1000+08:00) = 1000+08:00
</pre>

## 3\. java.time -> Date

This example shows you how to convert `LocalDate`, `LocalDateTime` and `ZonedDateTime` back to the classic `java.util.Date`

JavaTimeToDate.java

    package com.mkyong.java8;

    import java.time.*;
    import java.util.Date;

    public class JavaTimeToDate {

        public static void main(String[] args) {

            //Asia/Kuala_Lumpur +8
            ZoneId defaultZoneId = ZoneId.systemDefault();
            System.out.println("System Default TimeZone : " + defaultZoneId);

            LocalDate localDate = LocalDate.of(2016, 8, 19);
            Date date = Date.from(localDate.atStartOfDay(defaultZoneId).toInstant());
            System.out.println("\n1\. LocalDate -> Date");
            System.out.println("localDate : " + localDate);
            System.out.println("date : " + date);

            LocalDateTime localDateTime = LocalDateTime.of(2016,8,19,21,46,31);
            Date date2 = Date.from(localDateTime.atZone(defaultZoneId).toInstant());
            System.out.println("\n2\. LocalDateTime -> Date");
            System.out.println("localDateTime : " + localDateTime);
            System.out.println("date2 : " + date2);

            ZonedDateTime zonedDateTime = localDateTime.atZone(defaultZoneId);
            Date date3 = Date.from(zonedDateTime.toInstant());
            System.out.println("\n3\. ZonedDateTime -> Date");
            System.out.println("zonedDateTime : " + zonedDateTime);
            System.out.println("date3 : " + date3);

        }

    }

Output

    System Default TimeZone : Asia/Kuala_Lumpur

    1\. LocalDate -> Date
    localDate : 2016-08-19
    date : Fri Aug 19 00:00:00 MYT 2016

    2\. LocalDateTime -> Date
    localDateTime : 2016-08-19T21:46:31
    date2 : Fri Aug 19 21:46:31 MYT 2016

    3\. ZonedDateTime -> Date
    zonedDateTime : 2016-08-19T21:46:31+08:00[Asia/Kuala_Lumpur]
    date3 : Fri Aug 19 21:46:31 MYT 2016

## References

1.  [JSR 310: Date and Time API](https://jcp.org/en/jsr/detail?id=310)
2.  [Unix time](https://en.wikipedia.org/wiki/Unix_time)
3.  [Instant JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html)
4.  [Date JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/util/Date.html)
5.  [Java – Convert date and time between timezone](https://www.mkyong.com/java/java-convert-date-and-time-between-timezone/)

[http://www.mkyong.com/java8/java-8-convert-date-to-localdate-and-localdatetime/](http://www.mkyong.com/java8/java-8-convert-date-to-localdate-and-localdatetime/)
