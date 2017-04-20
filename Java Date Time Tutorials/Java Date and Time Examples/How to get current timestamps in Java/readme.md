To get the current timestamp in Java :

    Timestamp timestamp = new Timestamp(System.currentTimeMillis());
    //2016-11-16 06:43:19.77

Here are two Java examples to show you how to get current timestamps in Java. (Updated with Java 8)

## 1\. java.sql.Timestamp

Two methods to get the current `java.sql.Timestamp`

TimeStampExample.java

    package com.mkyong.date;

    import java.sql.Timestamp;
    import java.text.SimpleDateFormat;
    import java.util.Date;

    public class TimeStampExample {

        private static final SimpleDateFormat sdf = new SimpleDateFormat("yyyy.MM.dd.HH.mm.ss");

        public static void main(String[] args) {

            //method 1
            Timestamp timestamp = new Timestamp(System.currentTimeMillis());
            System.out.println(timestamp);

            //method 2 - via Date
            Date date = new Date();
            System.out.println(new Timestamp(date.getTime()));

            //return number of milliseconds since January 1, 1970, 00:00:00 GMT
            System.out.println(timestamp.getTime());

            //format timestamp
            System.out.println(sdf.format(timestamp));

        }

    }

Output

    2016-11-16 06:43:19.77
    2016-11-16 06:43:19.769
    1479249799770
    2016.11.16.06.43.19

## 2\. java.time.Instant

In Java 8, you can convert `java.sql.Timestamp` to the new `java.time.Instant`

InstantExample.java

    package com.mkyong.date;

    import java.sql.Timestamp;
    import java.time.Instant;

    public class InstantExample {

        public static void main(String[] args) {

            Timestamp timestamp = new Timestamp(System.currentTimeMillis());
            System.out.println(timestamp);

            //return number of milliseconds since January 1, 1970, 00:00:00 GMT
            System.out.println(timestamp.getTime());

            // Convert timestamp to instant
            Instant instant = timestamp.toInstant();
            System.out.println(instant);

            //return number of milliseconds since the epoch of 1970-01-01T00:00:00Z
            System.out.println(instant.toEpochMilli());

            // Convert instant to timestamp
            Timestamp tsFromInstant = Timestamp.from(instant);
            System.out.println(tsFromInstant.getTime());

        }

    }

Output

    2016-11-16 06:55:40.11
    1479250540110
    2016-11-15T22:55:40.110Z
    1479250540110
    1479250540110

## References

1.  [java.sql.Timestamp JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/sql/Timestamp.html)
2.  [java.time.Instant JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html)

[http://www.mkyong.com/java/how-to-get-current-timestamps-in-java/](http://www.mkyong.com/java/how-to-get-current-timestamps-in-java/)
