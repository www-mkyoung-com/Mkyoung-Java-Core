Few Java examples show you how to convert a String to the new Java 8 Date API – `java.time.LocalDate`

    DateTimeFormatter formatter = DateTimeFormatter.ofPattern("d/MM/yyyy");

    String date = "16/08/2016";

    //convert String to LocalDate
    LocalDate localDate = LocalDate.parse(date, formatter);

**Note**  
Refer to this official [DateTimeFormatter](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html) JavaDoc for more date time formatter examples.

**Note**  
You may interest at this classic `java.util.Date` example – [How to convert String to Date in Java](https://www.mkyong.com/java/how-to-convert-string-to-date-java/)

## 1\. String = 2016-08-16

If the String is formatted like [ISO_LOCAL_DATE](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html#ISO_LOCAL_DATE), you can parse the String directly, no need conversion.

TestNewDate1.java

    package com.mkyong.java8.date;

    import java.time.LocalDate;

    public class TestNewDate1 {

        public static void main(String[] argv) {

            String date = "2016-08-16";

    		//default, ISO_LOCAL_DATE
            LocalDate localDate = LocalDate.parse(date);

            System.out.println(localDate);

        }

    }

Output

    2016-08-16

## 2\. String = 16-Aug-2016

TestNewDate2.java

    package com.mkyong.java8.date;

    import java.time.LocalDate;
    import java.time.format.DateTimeFormatter;

    public class TestNewDate2 {

        public static void main(String[] argv) {

            DateTimeFormatter formatter = DateTimeFormatter.ofPattern("d-MMM-yyyy");

    		String date = "16-Aug-2016";

            LocalDate localDate = LocalDate.parse(date, formatter);

            System.out.println(localDate);  //default, print ISO_LOCAL_DATE

            System.out.println(formatter.format(localDate));

        }

    }

Output

    2016-08-16
    16-Aug-2016

## 3\. String = 16/08/2016

TestNewDate3.java

    package com.mkyong.java8.date;

    import java.time.LocalDate;
    import java.time.format.DateTimeFormatter;

    public class TestNewDate3 {

        public static void main(String[] argv) {

            DateTimeFormatter formatter = DateTimeFormatter.ofPattern("d/MM/yyyy");

            String date = "16/08/2016";

            LocalDate localDate = LocalDate.parse(date, formatter);

            System.out.println(localDate);

            System.out.println(formatter.format(localDate));

        }

    }

Output

    2016-08-16
    16/08/2016

## 4\. String = Tue, Aug 16 2016

TestNewDate4.java

    package com.mkyong.java8.date;

    import java.time.LocalDate;
    import java.time.format.DateTimeFormatter;

    public class TestNewDate4 {

        public static void main(String[] argv) {

            DateTimeFormatter formatter = DateTimeFormatter.ofPattern("E, MMM d yyyy");

            String date = "Tue, Aug 16 2016";

            LocalDate localDate = LocalDate.parse(date, formatter);

            System.out.println(localDate);

            System.out.println(formatter.format(localDate));

        }

    }

Output

    2016-08-16
    Tue, Aug 16 2016

## 5\. String = Tuesday, Aug 16, 2016 12:10:56 PM

This example convert a String to `java.time.LocalDateTime`

TestNewDate5.java

    package com.mkyong.java8.date;

    package com.mkyong.pageview;

    import java.time.LocalDateTime;
    import java.time.format.DateTimeFormatter;

    public class TestNewDate5 {

        public static void main(String[] argv) {

            DateTimeFormatter formatter = DateTimeFormatter.ofPattern("EEEE, MMM d, yyyy HH:mm:ss a");

            String date = "Tuesday, Aug 16, 2016 12:10:56 PM";

            LocalDateTime localDateTime = LocalDateTime.parse(date, formatter);

            System.out.println(localDateTime);

            System.out.println(formatter.format(localDateTime));

        }

    }

Output

    2016-08-16T12:10:56
    Tuesday, Aug 16, 2016 12:10:56 PM

## 6\. String = 2016-08-16T15:23:01Z

The ‘Z’ suffix means UTC, you can convert into a `java.time.instant` directly, then display it with a time zone.

TestNewDate6.java

    package com.mkyong.java8.date;

    import java.time.*;

    public class TestNewDate6 {

        public static void main(String[] argv) {

            String dateInString = "2016-08-16T15:23:01Z";

            Instant instant = Instant.parse(dateInString);

            System.out.println("Instant : " + instant);

            //get date time only
            LocalDateTime result = LocalDateTime.ofInstant(instant, ZoneId.of(ZoneOffset.UTC.getId()));

            //get localdate
            System.out.println("LocalDate : " + result.toLocalDate());

            //get date time + timezone
            ZonedDateTime zonedDateTime = instant.atZone(ZoneId.of("Asia/Tokyo"));
            System.out.println(zonedDateTime);

            //get date time + timezone
            ZonedDateTime zonedDateTime2 = instant.atZone(ZoneId.of("Europe/Athens"));
            System.out.println(zonedDateTime2);

        }

    }

Output

    Instant : 2016-08-16T15:23:01Z
    LocalDate : 2016-08-16
    2016-08-17T00:23:01+09:00[Asia/Tokyo]
    2016-08-16T18:23:01+03:00[Europe/Athens]

## 7\. String = 2016-08-16T10:15:30+08:00

String -> ZonedDateTime -> LocalDate

TestNewDate7.java

    package com.mkyong.java8.date;

    import java.time.*;
    import java.time.format.DateTimeFormatter;

    public class TestNewDate7 {

        public static void main(String[] argv) {

            String date = "2016-08-16T10:15:30+08:00";

            ZonedDateTime result = ZonedDateTime.parse(date, DateTimeFormatter.ISO_DATE_TIME);

            System.out.println("ZonedDateTime : " + result);

            System.out.println("TimeZone : " + result.getZone());

            LocalDate localDate = result.toLocalDate();

            System.out.println("LocalDate : " + localDate);

        }

    }

Output

    ZonedDateTime : 2016-08-16T10:15:30+08:00
    TimeZone : +08:00
    LocalDate : 2016-08-16

## References

1.  [DateTimeFormatter JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html)
2.  [Classic SimpleDateFormat JavaDoc](http://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html)
3.  [Java – How to convert String to Date](https://www.mkyong.com/java/how-to-convert-string-to-date-java/)
4.  [Stackoverflow : simpledateformat parsing date with ‘Z’ literal](http://stackoverflow.com/questions/2580925/simpledateformat-parsing-date-with-z-literal)
5.  [Wikipedia : ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)
6.  [GMT VS UTC](http://www.diffen.com/difference/GMT_vs_UTC)
7.  [What is a Time Zone?](http://www.timeanddate.com/time/what-is-a-time-zone.html)

[http://www.mkyong.com/java8/java-8-how-to-convert-string-to-localdate/](http://www.mkyong.com/java8/java-8-how-to-convert-string-to-localdate/)
