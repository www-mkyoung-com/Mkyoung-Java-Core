The **File.getAbsolutePath()** will give you the full complete path name (filepath + filename) of a file.

For example,

    File file = File("C:\\abcfolder\\textfile.txt");
    System.out.println("Path : " + file.getAbsolutePath());

It will display the full path : “**Path : C:\\abcfolder\\textfile.txt**“.

In most cases, you may just need to get the file path only “**C:\\abcfolder\\**“. With the help of **substring()** and **lastIndexOf()** menthods, you can extract the file path easily :

    File file = File("C:\\abcfolder\\textfile.txt");
    String absolutePath = file.getAbsolutePath();
    String filePath = absolutePath.
        substring(0,absolutePath.lastIndexOf(File.separator));

## Get file path example

In this example, it create a temporary file, and print out the file path of it.

    package com.mkyong.file;

    import java.io.File;
    import java.io.IOException;

    public class AbsoluteFilePathExample
    {
        public static void main(String[] args)
        {
        	try{

        	    File temp = File.createTempFile("i-am-a-temp-file", ".tmp" );

        	    String absolutePath = temp.getAbsolutePath();
        	    System.out.println("File path : " + absolutePath);

        	    String filePath = absolutePath.
        	    	     substring(0,absolutePath.lastIndexOf(File.separator));

        	    System.out.println("File path : " + filePath);

        	}catch(IOException e){

        	    e.printStackTrace();

        	}

        }
    }

## Result

    File path : C:\Users\mkyong\AppData\Local\Temp\i-am-a-temp-file69424.tmp
    File path : C:\Users\mkyong\AppData\Local\Temp

## Reference

1.  [File.getAbsolutePath() documentation](http://java.sun.com/j2se/1.4.2/docs/api/java/io/File.html)
2.  [String substring() and lastIndexOf() documentation](http://java.sun.com/j2se/1.4.2/docs/api/java/lang/String.html)

[http://www.mkyong.com/java/how-to-get-the-filepath-of-a-file-in-java/](http://www.mkyong.com/java/how-to-get-the-filepath-of-a-file-in-java/)
