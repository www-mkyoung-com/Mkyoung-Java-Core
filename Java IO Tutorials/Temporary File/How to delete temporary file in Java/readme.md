Temporary file is used to store the less important and temporary data, which should always be deleted when your system is terminated. The best practice is use the **File.deleteOnExit()** to do it.

For example,

    File temp = File.createTempFile("abc", ".tmp");
    temp.deleteOnExit();

The above example will create a temporary file named “**abc.tmp**” and delete it when the program is terminated or exited.

_P.S If you want to delete the temporary file manually, you can still use the **File.delete()**._

## Example

    package com.mkyong.file;

    import java.io.File;
    import java.io.IOException;

    public class DeleteTempFileExample
    {
        public static void main(String[] args)
        {

        	try{

        	   //create a temp file
        	   File temp = File.createTempFile("temptempfilefile", ".tmp");

        	   //delete temporary file when the program is exited
        	   temp.deleteOnExit();

               //delete immediate
        	   //temp.delete();

        	}catch(IOException e){

        	   e.printStackTrace();

        	}

        }
    }

[http://www.mkyong.com/java/how-to-delete-temporary-file-in-java/](http://www.mkyong.com/java/how-to-delete-temporary-file-in-java/)
