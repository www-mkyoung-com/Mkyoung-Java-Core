The **File.createNewFile()** method is used to create a file in Java, and return a boolean value : true if the file is created successful; false if the file is already exists or the operation failed.

    package com.mkyong.file;

    import java.io.File;
    import java.io.IOException;

    public class CreateFileExample
    {
        public static void main( String[] args )
        {
        	try {

    	      File file = new File("c:\\newfile.txt");

    	      if (file.createNewFile()){
    	        System.out.println("File is created!");
    	      }else{
    	        System.out.println("File already exists.");
    	      }

        	} catch (IOException e) {
    	      e.printStackTrace();
    	}
        }
    }

## Reference

1.  [http://java.sun.com/javase/6/docs/api/java/io/File.html](http://java.sun.com/javase/6/docs/api/java/io/File.html)
