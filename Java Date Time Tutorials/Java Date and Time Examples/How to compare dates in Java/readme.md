Few examples show you how to compare two dates in Java. Updated with Java 8 examples.

## 1\. Date.compareTo()

A classic method to compare two `java.util.Date` in Java.

1.  Return value is 0 if both dates are equal.
2.  Return value is greater than 0 , if Date is after the date argument.
3.  Return value is less than 0, if Date is before the date argument.

TestDate.java

    package com.mkyong.date;

    import java.text.ParseException;
    import java.text.SimpleDateFormat;
    import java.util.Date;

    public class TestDate {

        public static void main(String[] args) throws ParseException {

            SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
            Date date1 = sdf.parse("2009-12-31");
            Date date2 = sdf.parse("2010-01-31");

            System.out.println("date1 : " + sdf.format(date1));
            System.out.println("date2 : " + sdf.format(date2));

            if (date1.compareTo(date2) > 0) {
                System.out.println("Date1 is after Date2");
            } else if (date1.compareTo(date2) < 0) {
                System.out.println("Date1 is before Date2");
            } else if (date1.compareTo(date2) == 0) {
                System.out.println("Date1 is equal to Date2");
            } else {
                System.out.println("How to get here?");
            }

        }

    }

Output

    date1 : 2009-12-31
    date2 : 2010-01-31
    Date1 is before Date2

## 2\. Date.before(), Date.after() and Date.equals()

A more user friendly method to compare two `java.util.Date`

TestDate2.java

    package com.mkyong.date;

    import java.text.ParseException;
    import java.text.SimpleDateFormat;
    import java.util.Date;

    public class TestDate2 {

        public static void main(String[] args) throws ParseException {

            SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
            Date date1 = sdf.parse("2009-12-31");
            Date date2 = sdf.parse("2010-01-31");

            System.out.println("date1 : " + sdf.format(date1));
            System.out.println("date2 : " + sdf.format(date2));

            if (date1.after(date2)) {
                System.out.println("Date1 is after Date2");
            }

            if (date1.before(date2)) {
                System.out.println("Date1 is before Date2");
            }

            if (date1.equals(date2)) {
                System.out.println("Date1 is equal Date2");
            }

        }

    }

Output

    date1 : 2009-12-31
    date2 : 2010-01-31
    Date1 is before Date2

## 3\. Calender.before(), Calender.after() and Calender.equals()

Example to compare two `java.util.Calendar`

TestDate3.java

    package com.mkyong.date;

    import java.text.ParseException;
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    import java.util.Date;

    public class TestDate3 {

        public static void main(String[] args) throws ParseException {

            SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
            Date date1 = sdf.parse("2009-12-31");
            Date date2 = sdf.parse("2010-01-31");

            System.out.println("date1 : " + sdf.format(date1));
            System.out.println("date2 : " + sdf.format(date2));

            Calendar cal1 = Calendar.getInstance();
            Calendar cal2 = Calendar.getInstance();
            cal1.setTime(date1);
            cal2.setTime(date2);

            if (cal1.after(cal2)) {
                System.out.println("Date1 is after Date2");
            }

            if (cal1.before(cal2)) {
                System.out.println("Date1 is before Date2");
            }

            if (cal1.equals(cal2)) {
                System.out.println("Date1 is equal Date2");
            }
        }

    }

Output

    date1 : 2009-12-31
    date2 : 2010-01-31
    Date1 is before Date2

## 4\. Java 8

In Java 8, you can use the new isBefore(), isAfter(), isEqual() and compareTo() to compare LocalDate, LocalTime and LocalDateTime.

Review the following example to compare two `java.time.LocalDate`

TestDate4.java

    package com.mkyong.date;

    import java.time.LocalDate;
    import java.time.format.DateTimeFormatter;

    public class TestDate4 {

        public static void main(String[] args) {

            DateTimeFormatter sdf = DateTimeFormatter.ofPattern("yyyy-MM-dd");
            LocalDate date1 = LocalDate.of(2009, 12, 31);
            LocalDate date2 = LocalDate.of(2010, 01, 31);

            System.out.println("date1 : " + sdf.format(date1));
            System.out.println("date2 : " + sdf.format(date2));

            System.out.println("Is...");
            if (date1.isAfter(date2)) {
                System.out.println("Date1 is after Date2");
            }

            if (date1.isBefore(date2)) {
                System.out.println("Date1 is before Date2");
            }

            if (date1.isEqual(date2)) {
                System.out.println("Date1 is equal Date2");
            }

            System.out.println("CompareTo...");
            if (date1.compareTo(date2) > 0) {

                System.out.println("Date1 is after Date2");

            } else if (date1.compareTo(date2) < 0) {

                System.out.println("Date1 is before Date2");

            } else if (date1.compareTo(date2) == 0) {

                System.out.println("Date1 is equal to Date2");

            } else {

                System.out.println("How to get here?");

            }
        }

    }

Output

    date1 : 2009-12-31
    date2 : 2010-01-31
    Is...
    Date1 is before Date2
    CompareTo...
    Date1 is before Date2

## References

1.  [Date CompareTo JavaDoc](http://docs.oracle.com/javase/8/docs/api/java/util/Date.html#compareTo-java.util.Date-)
2.  [Calendar before after JavaDoc](http://docs.oracle.com/javase/8/docs/api/java/util/Calendar.html#before-java.lang.Object-)
3.  [LocalDate JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html)

[http://www.mkyong.com/java/how-to-compare-dates-in-java/](http://www.mkyong.com/java/how-to-compare-dates-in-java/)
