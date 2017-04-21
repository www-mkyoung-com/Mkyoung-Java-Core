A Java program to demonstrate the use of java.io.File **setReadOnly()** method to make a file read only. Since JDK 1.6, a new **setWritable()** method is provided to make a file to be writable again.

## Example

    package com.mkyong;

    import java.io.File;
    import java.io.IOException;

    public class FileReadAttribute
    {

        public static void main(String[] args) throws IOException
        {
        	File file = new File("c:/file.txt");

        	//mark this file as read only, since jdk 1.2
        	file.setReadOnly();

        	if(file.canWrite()){
        	     System.out.println("This file is writable");
        	}else{
        	     System.out.println("This file is read only");
        	}

        	//revert the operation, mark this file as writable, since jdk 1.6
        	file.setWritable(true);

        	if(file.canWrite()){
        	     System.out.println("This file is writable");
        	}else{
        	     System.out.println("This file is read only");
        	}
        }
    }

## Output

    This file is read only
    This file is writable

[http://www.mkyong.com/java/how-to-make-a-file-read-only-in-java/](http://www.mkyong.com/java/how-to-make-a-file-read-only-in-java/)
