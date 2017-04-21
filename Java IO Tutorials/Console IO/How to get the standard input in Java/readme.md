**Note**  
This post is duplicated, please refer to this – [3 ways to read input from console in Java](http://www.mkyong.com/java/how-to-read-input-from-console-java/).

A quick example to show you how to read the standard input in Java.

    package com.mkyong.pageview;

    import java.io.BufferedReader;
    import java.io.IOException;
    import java.io.InputStreamReader;

    public class Test {

        public static void main(String[] args) {

            BufferedReader br = null;

            try {

                // Refer to this http://www.mkyong.com/java/how-to-read-input-from-console-java/
                // for JDK 1.6, please use java.io.Console class to read system input.
                br = new BufferedReader(new InputStreamReader(System.in));

                while (true) {

                    System.out.print("Enter something : ");
                    String input = br.readLine();

                    if ("q".equals(input)) {
                        System.out.println("Exit!");
                        System.exit(0);
                    }

                    System.out.println("input : " + input);
                    System.out.println("-----------\n");
                }

            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                if (br != null) {
                    try {
                        br.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            }

        }

    }

[http://www.mkyong.com/java/how-to-get-the-standard-input-in-java/](http://www.mkyong.com/java/how-to-get-the-standard-input-in-java/)
