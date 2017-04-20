This article shows you how to add days to the current date, using the classic `java.util.Calendar` and the new Java 8 date and time APIs.

## 1\. Calendar.add

Example to add 1 year, 1 month, 1 day, 1 hour, 1 minute and 1 second to the current date.

DateExample.java

    package com.mkyong.time;

    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    import java.util.Date;

    public class DateExample {

        private static final DateFormat dateFormat = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");

        public static void main(String[] args) {

            Date currentDate = new Date();
            System.out.println(dateFormat.format(currentDate));

            // convert date to calendar
            Calendar c = Calendar.getInstance();
            c.setTime(currentDate);

            // manipulate date
            c.add(Calendar.YEAR, 1);
            c.add(Calendar.MONTH, 1);
            c.add(Calendar.DATE, 1); //same with c.add(Calendar.DAY_OF_MONTH, 1);
            c.add(Calendar.HOUR, 1);
            c.add(Calendar.MINUTE, 1);
            c.add(Calendar.SECOND, 1);

            // convert calendar to date
            Date currentDatePlusOne = c.getTime();

            System.out.println(dateFormat.format(currentDatePlusOne));

        }

    }

Output

    2016/11/10 17:11:48
    2017/12/11 18:12:49

## 2\. Java 8 Plus Minus

In Java 8, you can use the plus and minus methods to manipulate LocalDate, LocalDateTime and ZoneDateTime, see the following examples

LocalDateTimeExample.java

    package com.mkyong.time;

    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.time.LocalDateTime;
    import java.time.ZoneId;
    import java.time.format.DateTimeFormatter;
    import java.util.Date;

    public class LocalDateTimeExample {

        private static final String DATE_FORMAT = "yyyy/MM/dd HH:mm:ss";
        private static final DateFormat dateFormat = new SimpleDateFormat(DATE_FORMAT);
        private static final DateTimeFormatter dateFormat8 = DateTimeFormatter.ofPattern(DATE_FORMAT);

        public static void main(String[] args) {

    		// Get current date
            Date currentDate = new Date();
            System.out.println("date : " + dateFormat.format(currentDate));

            // convert date to localdatetime
            LocalDateTime localDateTime = currentDate.toInstant().atZone(ZoneId.systemDefault()).toLocalDateTime();
            System.out.println("localDateTime : " + dateFormat8.format(localDateTime));

            // plus one
            localDateTime = localDateTime.plusYears(1).plusMonths(1).plusDays(1);
            localDateTime = localDateTime.plusHours(1).plusMinutes(2).minusMinutes(1).plusSeconds(1);

            // convert LocalDateTime to date
            Date currentDatePlusOneDay = Date.from(localDateTime.atZone(ZoneId.systemDefault()).toInstant());

            System.out.println("\nOutput : " + dateFormat.format(currentDatePlusOneDay));

        }

    }

Output

    date : 2016/11/10 17:40:11
    localDateTime : 2016/11/10 17:40:11

    Output : 2017/12/11 18:41:12

## References

1.  [Calendar JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/util/Calendar.html)
2.  [Java – How to get current date time – date() and calender()](https://www.mkyong.com/java/java-how-to-get-current-date-time-date-and-calender/)
3.  [Java 8 – Convert Date to LocalDate and LocalDateTime](https://www.mkyong.com/java8/java-8-convert-date-to-localdate-and-localdatetime/)

[http://www.mkyong.com/java/java-how-to-add-days-to-current-date/](http://www.mkyong.com/java/java-how-to-add-days-to-current-date/)
