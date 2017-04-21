No nonsense, just issue the **File.delete()** to delete a file, it will return a boolean value to indicate the delete operation status; true if the file is deleted; false if failed.

## Example

In this example, it will delete a log file named “c:\\logfile20100131.log”.

    package com.mkyong.file;

    import java.io.File;

    public class DeleteFileExample
    {
        public static void main(String[] args)
        {
        	try{

        		File file = new File("c:\\logfile20100131.log");

        		if(file.delete()){
        			System.out.println(file.getName() + " is deleted!");
        		}else{
        			System.out.println("Delete operation is failed.");
        		}

        	}catch(Exception e){

        		e.printStackTrace();

        	}

        }
    }

[http://www.mkyong.com/java/how-to-delete-file-in-java/](http://www.mkyong.com/java/how-to-delete-file-in-java/)
