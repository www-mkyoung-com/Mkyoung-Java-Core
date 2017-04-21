In Java, you can use the **File.lastModified()** to get the file’s last modified timestamps. This method will returns the time in milliseconds (long value), you may to format it with **SimpleDateFormat** to make it a human readable format.

## File Last Modified

    package com.mkyong.file;

    import java.io.File;
    import java.text.SimpleDateFormat;

    public class GetFileLastModifiedExample
    {
        public static void main(String[] args)
        {
    	File file = new File("c:\\logfile.log");

    	System.out.println("Before Format : " + file.lastModified());

    	SimpleDateFormat sdf = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");

    	System.out.println("After Format : " + sdf.format(file.lastModified()));
        }
    }

## Result

    Before Format : 1275265349422
    After Format : 05/31/2010 08:22:29

[http://www.mkyong.com/java/how-to-get-the-file-last-modified-date-in-java/](http://www.mkyong.com/java/how-to-get-the-file-last-modified-date-in-java/)
