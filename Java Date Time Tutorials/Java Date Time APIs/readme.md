In old days, we use the following classic Date and Calendar APIs to represent and manipulate date.

*   `java.util.Date` – date and time, print with default time-zone.
*   `java.util.Calendar` – date and time, more methods to manipulate date.
*   `java.text.SimpleDateFormat` – formatting (date -> text), parsing (text -> date) for date and calendar.

In Java 8, a new series of date and time APIs ([JSR310](https://jcp.org/en/jsr/detail?id=310) and inspired by Joda-time) are created in the new `java.time`package.

*   `java.time.LocalDate` – date without time, no time-zone.
*   `java.time.LocalTime` – time without date, no time-zone.
*   `java.time.LocalDateTime` – date and time, no time-zone.
*   `java.time.ZonedDateTime` – date and time, with time-zone.
*   `java.time.DateTimeFormatter` – formatting (date -> text), parsing (text -> date) for java.time
*   `java.time.Instant` – date and time for machine, seconds passed since the Unix epoch time (midnight of January 1, 1970 UTC)
*   `java.time.Duration` – Measures time in seconds and nanoseconds.
*   `java.time.Period` – Measures time in years, months and days.
*   `java.time.TemporalAdjuster` – Adjust date.

**Note**  
Read Oracle article – [Why do we need a new date and time library?](http://www.oracle.com/technetwork/articles/java/jf14-date-time-2125367.html)
