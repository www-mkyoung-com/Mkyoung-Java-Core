Here’s an example to write data to temporary file in Java. Actually, there are no different between normal file and temporary file, what apply to normal text file, will apply to temporary file as well.

## Example

In this example, it will create a temporary file named “**tempfile.tmp**“, and write the text “This is the temporary file content” inside.

    package com.mkyong.file;

    import java.io.BufferedWriter;
    import java.io.File;
    import java.io.FileWriter;
    import java.io.IOException;

    public class WriteTempFileExample
    {
        public static void main(String[] args)
        {

        	try{

        	    //create a temp file
        	    File temp = File.createTempFile("tempfile", ".tmp");

    	    //write it
        	    BufferedWriter bw = new BufferedWriter(new FileWriter(temp));
        	    bw.write("This is the temporary file content");
        	    bw.close();

        	    System.out.println("Done");

        	}catch(IOException e){

        	    e.printStackTrace();

        	}

        }
    }

[http://www.mkyong.com/java/how-to-write-data-to-temporary-file-in-java/](http://www.mkyong.com/java/how-to-write-data-to-temporary-file-in-java/)
