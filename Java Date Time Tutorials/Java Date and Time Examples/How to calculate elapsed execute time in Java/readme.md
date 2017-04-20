In Java, you can use the following ways to measure elapsed time in Java.

## 1\. System.nanoTime()

This is the recommended solution to measure elapsed time in Java.

ExecutionTime1.java

    package com.mkyong.time;

    import java.util.concurrent.TimeUnit;

    public class ExecutionTime1 {

        public static void main(String[] args) throws InterruptedException {

    		//start
            long lStartTime = System.nanoTime();

    		//task
            calculation();

    		//end
            long lEndTime = System.nanoTime();

    		//time elapsed
            long output = lEndTime - lStartTime;

            System.out.println("Elapsed time in milliseconds: " + output / 1000000);

        }

        private static void calculation() throws InterruptedException {

            //Sleep 2 seconds
            TimeUnit.SECONDS.sleep(2);

        }
    }

Output may vary.

    2004

## 2\. System.currentTimeMillis()

ExecutionTime2.java

    package com.mkyong.time;

    import java.util.concurrent.TimeUnit;

    public class ExecutionTime2 {

        public static void main(String[] args) throws InterruptedException {

            long lStartTime = System.currentTimeMillis();

            calculation();

            long lEndTime = System.currentTimeMillis();

            long output = lEndTime - lStartTime;

            System.out.println("Elapsed time in milliseconds: " + output);

        }

        private static void calculation() throws InterruptedException {

            //Sleep 2 seconds
            TimeUnit.SECONDS.sleep(2);

        }
    }

Output may vary.

    2006

## 3\. Instant.now().toEpochMilli()

In Java 8, you can try the new `java.time.Instant`

ExecutionTime3.java

    package com.mkyong.time;

    import java.time.Instant;
    import java.util.concurrent.TimeUnit;

    public class ExecutionTime3 {

        public static void main(String[] args) throws InterruptedException {

            long lStartTime = Instant.now().toEpochMilli();

            calculation();

            long lEndTime = Instant.now().toEpochMilli();

            long output = lEndTime - lStartTime;

            System.out.println("Elapsed time in milliseconds: " + output);

        }

        private static void calculation() throws InterruptedException {

            //Sleep 2 seconds
            TimeUnit.SECONDS.sleep(2);

        }
    }

Output may vary.

    2006

## 4\. Date().getTime()

ExecutionTime4.java

    package com.mkyong.time;

    import java.util.Date;
    import java.util.concurrent.TimeUnit;

    public class ExecutionTime4 {

        public static void main(String[] args) throws InterruptedException {

            long lStartTime = new Date().getTime();

            calculation();

            long lEndTime = new Date().getTime();

            long output = lEndTime - lStartTime;

            System.out.println("Elapsed time in milliseconds: " + output);

        }

        private static void calculation() throws InterruptedException {

            //Sleep 2 seconds
            TimeUnit.SECONDS.sleep(2);

        }
    }

Output may vary.

    2007

## References

1.  [Stackoverflow – Is System.nanoTime() completely useless?](http://stackoverflow.com/questions/510462/is-system-nanotime-completely-useless)
2.  [Stackoverflow – System.currentTimeMillis vs System.nanoTime](http://stackoverflow.com/questions/351565/system-currenttimemillis-vs-system-nanotime)
3.  [System#nanoTime JavaDoc](http://docs.oracle.com/javase/8/docs/api/java/lang/System.html#nanoTime--)
4.  [Instant#toEpochMilli JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html#toEpochMilli--)

[http://www.mkyong.com/java/how-do-calculate-elapsed-execute-time-in-java/](http://www.mkyong.com/java/how-do-calculate-elapsed-execute-time-in-java/)
