The **LineNumberReader** class is a useful class to handle the lines of a file, you can loop the **LineNumberReader.readLine()** method and accumulate it as the total number of lines. A line is considered a line if it ends with a **line feed (‘\n’)** or a **carriage return (‘\r’)**.

## Example

A text file named “c:\\ihave10lines.txt”, contains 10 lines

    Line 1
    Line 2
    Line 3
    Line 4
    Line 5
    Line 6
    Line 7
    Line 8
    Line 9
    Line 10

Counts the line

    package com.mkyong.file;

    import java.io.File;
    import java.io.FileReader;
    import java.io.IOException;
    import java.io.LineNumberReader;

    public class LineNumberReaderExample
    {
        public static void main(String[] args)
        {

        	try{

        		File file =new File("c:\\ihave10lines.txt");

        		if(file.exists()){

        		    FileReader fr = new FileReader(file);
        		    LineNumberReader lnr = new LineNumberReader(fr);

        		    int linenumber = 0;

        	            while (lnr.readLine() != null){
        	        	linenumber++;
        	            }

        	            System.out.println("Total number of lines : " + linenumber);

        	            lnr.close();

        		}else{
        			 System.out.println("File does not exists!");
        		}

        	}catch(IOException e){
        		e.printStackTrace();
        	}

        }
    }

## Result

    Total number of lines : 10

## Reference

1.  [LineNumberReader Java Doc](http://java.sun.com/javase/6/docs/api/java/io/LineNumberReader.html)

[http://www.mkyong.com/java/how-to-get-the-total-number-of-lines-of-a-file-in-java/](http://www.mkyong.com/java/how-to-get-the-total-number-of-lines-of-a-file-in-java/)
