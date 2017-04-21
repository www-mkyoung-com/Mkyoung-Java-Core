A Java program to demonstrate the use of java.io.File **isHidden()** to check if a file is hidden.

    package com.mkyong;

    import java.io.File;
    import java.io.IOException;

    public class FileHidden
    {

        public static void main(String[] args) throws IOException
        {
        	File file = new File("c:/hidden-file.txt");

        	if(file.isHidden()){
        		System.out.println("This file is hidden");
        	}else{
        		System.out.println("This file is not hidden");
        	}
        }
    }

[http://www.mkyong.com/java/how-to-check-if-a-file-is-hidden-in-java/](http://www.mkyong.com/java/how-to-check-if-a-file-is-hidden-in-java/)
