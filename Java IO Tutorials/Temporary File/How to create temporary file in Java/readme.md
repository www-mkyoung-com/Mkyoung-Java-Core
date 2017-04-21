Here’s an example to create a temporary file in Java.

## Example

    package com.mkyong.file;

    import java.io.File;
    import java.io.IOException;

    public class CreateTempFileExample
    {
        public static void main(String[] args)
        {

        	try{

        	   //create a temp file
        	   File temp = File.createTempFile("temp-file-name", ".tmp");

        	   System.out.println("Temp file : " + temp.getAbsolutePath());

        	}catch(IOException e){

        	   e.printStackTrace();

        	}

        }
    }

## Result

    Temp file : C:\Users\mkyong\AppData\Local\Temp\temp-file-name623426.tmp

[http://www.mkyong.com/java/how-to-create-temporary-file-in-java/](http://www.mkyong.com/java/how-to-create-temporary-file-in-java/)
