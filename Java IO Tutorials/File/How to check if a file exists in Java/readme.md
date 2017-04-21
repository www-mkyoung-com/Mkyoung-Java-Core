To determine whether a file is exist in your file system, use the Java IO **File.exists()**.

    package com.mkyong.io;

    import java.io.*;

    public class FileChecker {

      public static void main(String args[]) {

    	  File f = new File("c:\\mkyong.txt");

    	  if(f.exists()){
    		  System.out.println("File existed");
    	  }else{
    		  System.out.println("File not found!");
    	  }

      }

    }

[http://www.mkyong.com/java/how-to-check-if-a-file-exists-in-java/](http://www.mkyong.com/java/how-to-check-if-a-file-exists-in-java/)
