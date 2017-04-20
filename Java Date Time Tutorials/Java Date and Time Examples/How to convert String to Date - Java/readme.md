In this tutorial, we will show you how to convert a String to `java.util.Date`. Many Java beginners are stuck in the Date conversion, hope this summary guide will helps you in some ways.

    // String -> Date
    SimpleDateFormat.parse(String);

    // Date -> String
    SimpleDateFormat.format(date);

Refer to table below for some of the common date and time patterns used in `java.text.SimpleDateFormat`, refer to this [JavaDoc](http://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html)

LetterDescriptionExamplesyYear2013MMonth in yearJuly, 07, 7dDay in month1-31EDay name in weekFriday, SundayaAm/pm markerAM, PMHHour in day0-23hHour in am/pm1-12mMinute in hour0-60sSecond in minute0-60

**Note**  
You may interest at this Java 8 example – [How to convert String to LocalDate](http://www.mkyong.com/java8/java-8-how-to-convert-string-to-localdate/)

## 1\. String = 7-Jun-2013

If 3 ‘M’, then the month is interpreted as text (Mon-Dec), else number (01-12).

TestDateExample1.java

    package com.mkyong.date;

    import java.text.ParseException;
    import java.text.SimpleDateFormat;
    import java.util.Date;

    public class TestDateExample1 {

        public static void main(String[] argv) {

            SimpleDateFormat formatter = new SimpleDateFormat("dd-MMM-yyyy");
            String dateInString = "7-Jun-2013";

            try {

                Date date = formatter.parse(dateInString);
                System.out.println(date);
                System.out.println(formatter.format(date));

            } catch (ParseException e) {
                e.printStackTrace();
            }

        }

    }

Output

    Fri Jun 07 00:00:00 MYT 2013
    07-Jun-2013

## 2\. String = 07/06/2013

TestDateExample2.java

    package com.mkyong.date;

    import java.text.ParseException;
    import java.text.SimpleDateFormat;
    import java.util.Date;

    public class TestDateExample2 {

        public static void main(String[] argv) {

            SimpleDateFormat formatter = new SimpleDateFormat("dd/MM/yyyy");
            String dateInString = "07/06/2013";

            try {

                Date date = formatter.parse(dateInString);
                System.out.println(date);
                System.out.println(formatter.format(date));

            } catch (ParseException e) {
                e.printStackTrace();
            }

        }

    }

Output

    Fri Jun 07 00:00:00 MYT 2013
    07/06/2013

## 3\. String = Fri, June 7 2013

TestDateExample3.java

    package com.mkyong.date;

    import java.text.ParseException;
    import java.text.SimpleDateFormat;
    import java.util.Date;

    public class TestDateExample3 {

        public static void main(String[] argv) {

            SimpleDateFormat formatter = new SimpleDateFormat("E, MMM dd yyyy");
            String dateInString = "Fri, June 7 2013";

            try {

                Date date = formatter.parse(dateInString);
                System.out.println(date);
                System.out.println(formatter.format(date));

            } catch (ParseException e) {
                e.printStackTrace();
            }

        }

    }

Output

    Fri Jun 07 00:00:00 MYT 2013
    Fri, Jun 07 2013

## 4\. String = Friday, Jun 7, 2013 12:10:56 PM

TestDateExample4.java

    package com.mkyong.date;

    import java.text.ParseException;
    import java.text.SimpleDateFormat;
    import java.util.Date;

    public class TestDateExample4 {

        public static void main(String[] argv) {

            SimpleDateFormat formatter = new SimpleDateFormat("EEEE, MMM dd, yyyy HH:mm:ss a");
            String dateInString = "Friday, Jun 7, 2013 12:10:56 PM";

            try {

                Date date = formatter.parse(dateInString);
                System.out.println(date);
                System.out.println(formatter.format(date));

            } catch (ParseException e) {
                e.printStackTrace();
            }

        }

    }

Output

    Fri Jun 07 12:10:56 MYT 2013
    Friday, Jun 07, 2013 12:10:56 PM

## 5\. String = 2014-10-05T15:23:01Z

Z suffix means UTC, `java.util.SimpleDateFormat` doesn’t parse it correctly, you need to replace the suffix Z with ‘+0000’.

TestDateExample5.java

    package com.mkyong.date;

    import java.text.ParseException;
    import java.text.SimpleDateFormat;
    import java.util.Date;

    public class TestDateExample5 {

        public static void main(String[] argv) {

            SimpleDateFormat formatter = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssZ");
            String dateInString = "2014-10-05T15:23:01Z";

            try {

                Date date = formatter.parse(dateInString.replaceAll("Z$", "+0000"));
                System.out.println(date);

                System.out.println("time zone : " + TimeZone.getDefault().getID());
                System.out.println(formatter.format(date));

            } catch (ParseException e) {
                e.printStackTrace();
            }

        }

    }

Output

    Sun Oct 05 23:23:01 MYT 2014
    time zone : Asia/Kuala_Lumpur
    2014-10-05T23:23:01+0800

In Java 8, you can convert it into a `java.time.Instant` object, and display it with a specified time zone.

TestDateExample6.java

    package com.mkyong.date;

    import java.time.*;

    public class TestDateExample6 {

        public static void main(String[] argv) {

            String dateInString = "2014-10-05T15:23:01Z";

            Instant instant = Instant.parse(dateInString);

            System.out.println(instant);

            //get date time only
            LocalDateTime result = LocalDateTime.ofInstant(instant, ZoneId.of(ZoneOffset.UTC.getId()));

            System.out.println(result);

            //get date time + timezone
            ZonedDateTime zonedDateTime = instant.atZone(ZoneId.of("Africa/Tripoli"));
            System.out.println(zonedDateTime);

            //get date time + timezone
            ZonedDateTime zonedDateTime2 = instant.atZone(ZoneId.of("Europe/Athens"));
            System.out.println(zonedDateTime2);

        }

    }

Output

    2014-10-05T15:23:01Z
    2014-10-05T15:23:01
    2014-10-05T17:23:01+02:00[Africa/Tripoli]
    2014-10-05T18:23:01+03:00[Europe/Athens]

## References

1.  [SimpleDateFormat JavaDoc](http://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html)
2.  [Java 8 – How to convert String to LocalDate](http://www.mkyong.com/java8/java-8-how-to-convert-string-to-localdate/)
3.  [Stackoverflow : simpledateformat parsing date with ‘Z’ literal](http://stackoverflow.com/questions/2580925/simpledateformat-parsing-date-with-z-literal)
4.  [Wikipedia : ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)
5.  [Time Zone and Offset Classes](https://docs.oracle.com/javase/tutorial/datetime/iso/timezones.html)
6.  [GMT VS UTC](http://www.diffen.com/difference/GMT_vs_UTC)
7.  [What is a Time Zone?](http://www.timeanddate.com/time/what-is-a-time-zone.html)
8.  [Joda Time](http://www.joda.org/joda-time/)

[http://www.mkyong.com/java/how-to-convert-string-to-date-java/](http://www.mkyong.com/java/how-to-convert-string-to-date-java/)
