Here’s an example to get the temporary file path in Java.

## Example

    package com.mkyong.file;

    import java.io.File;
    import java.io.IOException;

    public class GetTempFilePathExample
    {
        public static void main(String[] args)
        {

        	try{

        		//create a temp file
        		File temp = File.createTempFile("temp-file-name", ".tmp");

        		System.out.println("Temp file : " + temp.getAbsolutePath());

    		//Get tempropary file path
        		String absolutePath = temp.getAbsolutePath();
        		String tempFilePath = absolutePath.
        		    substring(0,absolutePath.lastIndexOf(File.separator));

        		System.out.println("Temp file path : " + tempFilePath);

        	}catch(IOException e){

        		e.printStackTrace();

        	}

        }
    }

## Result

    Temp file : C:\Users\mkyong\AppData\Local\Temp\temp-file-name79456440.tmp
    Temp file path : C:\Users\mkyong\AppData\Local\Temp

[http://www.mkyong.com/java/how-to-get-the-temporary-file-path-in-java/](http://www.mkyong.com/java/how-to-get-the-temporary-file-path-in-java/)
