![Calendar](http://www.mkyong.com/wp-content/uploads/2013/10/Calendar.png)

This tutorial shows you how to work with `java.util.Date` and `java.util.Calendar`.

## 1\. Java Date Examples

Few examples to work with `Date` APIs.

**Example 1.1** – Convert Date to String.

    SimpleDateFormat sdf = new SimpleDateFormat("dd/M/yyyy");
    String date = sdf.format(new Date());
    System.out.println(date); //15/10/2013

**Example 1.2** – Convert String to Date.

    SimpleDateFormat sdf = new SimpleDateFormat("dd-M-yyyy hh:mm:ss");
    String dateInString = "31-08-1982 10:20:56";
    Date date = sdf.parse(dateInString);
    System.out.println(date); //Tue Aug 31 10:20:56 SGT 1982

_P.S Refer to this – [SimpleDateFormat JavaDoc](http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html) for detail date and time patterns._

**Example 1.3** – Get current date time

    SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");
    Date date = new Date();
    System.out.println(dateFormat.format(date)); //2013/10/15 16:16:39

**Example 1.4** – Convert Calendar to Date

    Calendar calendar = Calendar.getInstance();
            Date date =  calendar.getTime();

## 2\. Java Calendar Examples

Few examples to work with `Calendar` APIs.

**Example 2.1** – Get current date time

    SimpleDateFormat sdf = new SimpleDateFormat("yyyy MMM dd HH:mm:ss");
    Calendar calendar = new GregorianCalendar(2013,0,31);
    System.out.println(sdf.format(calendar.getTime()));

Output

    2013 Jan 31 00:00:00

**Example 2.2** – Simple Calendar example

    SimpleDateFormat sdf = new SimpleDateFormat("yyyy MMM dd HH:mm:ss");
    Calendar calendar = new GregorianCalendar(2013,1,28,13,24,56);

    int year       = calendar.get(Calendar.YEAR);
    int month      = calendar.get(Calendar.MONTH); // Jan = 0, dec = 11
    int dayOfMonth = calendar.get(Calendar.DAY_OF_MONTH);
    int dayOfWeek  = calendar.get(Calendar.DAY_OF_WEEK);
    int weekOfYear = calendar.get(Calendar.WEEK_OF_YEAR);
    int weekOfMonth= calendar.get(Calendar.WEEK_OF_MONTH);

    int hour       = calendar.get(Calendar.HOUR);        // 12 hour clock
    int hourOfDay  = calendar.get(Calendar.HOUR_OF_DAY); // 24 hour clock
    int minute     = calendar.get(Calendar.MINUTE);
    int second     = calendar.get(Calendar.SECOND);
    int millisecond= calendar.get(Calendar.MILLISECOND);

    System.out.println(sdf.format(calendar.getTime()));

    System.out.println("year \t\t: " + year);
    System.out.println("month \t\t: " + month);
    System.out.println("dayOfMonth \t: " + dayOfMonth);
    System.out.println("dayOfWeek \t: " + dayOfWeek);
    System.out.println("weekOfYear \t: " + weekOfYear);
    System.out.println("weekOfMonth \t: " + weekOfMonth);

    System.out.println("hour \t\t: " + hour);
    System.out.println("hourOfDay \t: " + hourOfDay);
    System.out.println("minute \t\t: " + minute);
    System.out.println("second \t\t: " + second);
    System.out.println("millisecond \t: " + millisecond);

Output

    2013 Feb 28 13:24:56
    year 		: 2013
    month 		: 1
    dayOfMonth 	: 28
    dayOfWeek 	: 5
    weekOfYear 	: 9
    weekOfMonth     : 5
    hour 		: 1
    hourOfDay 	: 13
    minute 		: 24
    second 		: 56
    millisecond     : 0

**Example 2.3** – Set a date manually.

    SimpleDateFormat sdf = new SimpleDateFormat("yyyy MMM dd HH:mm:ss");

    Calendar calendar = new GregorianCalendar(2013,1,28,13,24,56);
    System.out.println("#1\. " + sdf.format(calendar.getTime()));

    //update a date
    calendar.set(Calendar.YEAR, 2014);
    calendar.set(Calendar.MONTH, 11);
    calendar.set(Calendar.MINUTE, 33);

    System.out.println("#2\. " + sdf.format(calendar.getTime()));

Output

    #1\. 2013 Feb 28 13:24:56
    #2\. 2014 Dec 28 13:33:56

**Example 2.4**– Add or subtract from a date.

    SimpleDateFormat sdf = new SimpleDateFormat("yyyy MMM dd");

    Calendar calendar = new GregorianCalendar(2013,10,28);
    System.out.println("Date : " + sdf.format(calendar.getTime()));

    //add one month
    calendar.add(Calendar.MONTH, 1);
    System.out.println("Date : " + sdf.format(calendar.getTime()));

    //subtract 10 days
    calendar.add(Calendar.DAY_OF_MONTH, -10);
    System.out.println("Date : " + sdf.format(calendar.getTime()));

Output

    Date : 2013 Nov 28
    Date : 2013 Dec 28
    Date : 2013 Dec 18

**Example 2.5**– Convert Date to Calendar.

    SimpleDateFormat sdf = new SimpleDateFormat("dd-M-yyyy hh:mm:ss");
    String dateInString = "22-01-2015 10:20:56";
    Date date = sdf.parse(dateInString);

            Calendar calendar = Calendar.getInstance();
    calendar.setTime(date);

## References

1.  [Calendar JavaDoc](http://docs.oracle.com/javase/7/docs/api/java/util/Calendar.html)
2.  [Date JavaDoc](http://docs.oracle.com/javase/6/docs/api/java/util/Date.html)
3.  [Java – Convert String to Date](http://www.mkyong.com/java/how-to-convert-string-to-date-java/)
4.  [How To Compare Dates In Java](http://www.mkyong.com/java/how-to-compare-dates-in-java/)

[https://www.mkyong.com/java/java-date-and-calendar-examples/](https://www.mkyong.com/java/java-date-and-calendar-examples/)
