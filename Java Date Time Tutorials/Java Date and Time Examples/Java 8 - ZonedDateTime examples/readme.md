![paris-time-zone](http://www.mkyong.com/wp-content/uploads/2016/08/paris-time-zone.png)

Few `java.time.ZonedDateTime` examples to show you how to convert a time zone between different countries.

## 1\. Malaysia (KUL) -> Japan (HND)

Review a flight information from Malaysia Kuala Lumpur (UTC+08:00) to Japan Tokyo Haneda (UTC+09:00)

<pre>---Flight Detail---
Kuala Lumpur (KUL) -> Tokyo Haneda (HND)
Flight Duration : 7 hours

(KUL-Depart) 1430, 22 Aug 2016 ->  2230, 22 Aug 2016 (HND-Arrive)
</pre>

_P.S Japan Tokyo is one hour faster than Malaysia Kuala lumpur_

DifferentTimeZoneExample1.java

    package com.mkyong.timezone;

    import java.time.LocalDateTime;
    import java.time.Month;
    import java.time.ZoneId;
    import java.time.ZonedDateTime;
    import java.time.format.DateTimeFormatter;

    public class DifferentTimeZoneExample1 {

        public static void main(String[] args) {

            DateTimeFormatter format = DateTimeFormatter.ofPattern("HHmm, dd MMM yyyy");

            LocalDateTime ldt = LocalDateTime.of(2016, Month.AUGUST, 22, 14, 30);
            System.out.println("LocalDateTime : " + format.format(ldt));

            //UTC+8
            ZonedDateTime klDateTime = ldt.atZone(ZoneId.of("Asia/Kuala_Lumpur"));
            System.out.println("Depart : " + format.format(klDateTime));

            //UTC+9 and flight duration = 7 hours
            ZonedDateTime japanDateTime = klDateTime.withZoneSameInstant(ZoneId.of("Asia/Tokyo")).plusHours(7);
            System.out.println("Arrive : " + format.format(japanDateTime));

            System.out.println("\n---Detail---");
            System.out.println("Depart : " + klDateTime);
            System.out.println("Arrive : " + japanDateTime);

        }

    }

Output

    LocalDateTime : 1430, 22 Aug 2016
    Depart : 1430, 22 Aug 2016
    Arrive : 2230, 22 Aug 2016

    ---Detail---
    Depart : 2016-08-22T14:30+08:00[Asia/Kuala_Lumpur]
    Arrive : 2016-08-22T22:30+09:00[Asia/Tokyo]

## 2\. France, Paris -> -05:00

Another time zone example from France, Paris (UTC+02:00, DST) to a hard coded (UTC-05:00) time zone (e.g New York)

<pre>---Flight Detail---
France, Paris -> UTC-05:00
Flight Duration : 8 hours 10 minutes

(Depart) 1430, 22 Aug 2016 ->  1540, 22 Aug 2016 (Arrive)
</pre>

DifferentTimeZoneExample2.java

    package com.mkyong.timezone;

    import java.time.LocalDateTime;
    import java.time.ZoneId;
    import java.time.ZoneOffset;
    import java.time.ZonedDateTime;
    import java.time.format.DateTimeFormatter;

    public class DifferentTimeZoneExample2 {

        public static void main(String[] args) {

            DateTimeFormatter format = DateTimeFormatter.ofPattern("HHmm, dd MMM yyyy");

            //Convert String to LocalDateTime
            String date = "2016-08-22 14:30";
            LocalDateTime ldt = LocalDateTime.parse(date, DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm"));
            System.out.println("LocalDateTime : " + format.format(ldt));

            //Paris, 2016 Apr-Oct = DST, UTC+2, other months UTC+1
            //UTC+2
            ZonedDateTime parisDateTime = ldt.atZone(ZoneId.of("Europe/Paris"));
            System.out.println("Depart : " + format.format(parisDateTime));

            //hard code a zoneoffset like this, UTC-5
            ZoneOffset nyOffSet = ZoneOffset.of("-05:00");
            ZonedDateTime nyDateTime = parisDateTime.withZoneSameInstant(nyOffSet).plusHours(8).plusMinutes(10);
            System.out.println("Arrive : " + format.format(nyDateTime));

            System.out.println("\n---Detail---");
            System.out.println("Depart : " + parisDateTime);
            System.out.println("Arrive : " + nyDateTime);

        }

    }

Output

    LocalDateTime : 1430, 22 Aug 2016
    Depart : 1430, 22 Aug 2016
    Arrive : 1540, 22 Aug 2016

    ---Detail---
    Depart : 2016-08-22T14:30+02:00[Europe/Paris]
    Arrive : 2016-08-22T15:40-05:00

**Daylight Saving Time (DST)**  
Paris, normally UTC+1 has DST (add one hour = UTC+2) from 27/mar to 30/Oct, 2016\. Review the above output, the `java.time` is able to calculate and handle the DST correctly.

## References

1.  [Wikipedia – Daylight saving time](https://en.wikipedia.org/wiki/Daylight_saving_time)
2.  [DateTimeFormatter JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html)
3.  [ZoneddateTime JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/ZonedDateTime.html)
4.  [Time Zone in Paris](http://www.timeanddate.com/time/zone/france/paris)
5.  [Airasia – Flight information](http://www.airasia.com/)
6.  [Java 8 – Convert Instant to ZonedDateTime](http://www.mkyong.com/java8/java-8-convert-instant-to-zoneddatetime/)
7.  [Java – Convert date and time between timezone](https://www.mkyong.com/java/java-convert-date-and-time-between-timezone/)
8.  [Java 8 – How to convert String to LocalDate](http://www.mkyong.com/java8/java-8-how-to-convert-string-to-localdate/)

[http://www.mkyong.com/java8/java-8-zoneddatetime-examples/](http://www.mkyong.com/java8/java-8-zoneddatetime-examples/)
