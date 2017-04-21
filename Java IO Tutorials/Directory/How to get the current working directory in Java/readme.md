The current working directory means the root folder of your current Java project, it can be retrieved by using the following system property function.

    String workingDir = System.getProperty("user.dir");

## Example

    package com.mkyong.io;

    public class App{

       public static void main (String args[]) {

    	   String workingDir = System.getProperty("user.dir");
    	   System.out.println("Current working directory : " + workingDir);

       }
    }

Output

    Current working directory : E:\workspace\HibernateExample

[http://www.mkyong.com/java/how-to-get-the-current-working-directory-in-java/](http://www.mkyong.com/java/how-to-get-the-current-working-directory-in-java/)
