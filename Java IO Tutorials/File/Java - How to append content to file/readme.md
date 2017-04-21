In Java, you can use `FileWriter(file,true)` to append new content to the end of a file.

1\. All existing content will be overridden.

    new FileWriter(file);

2\. Keep the existing content and append the new content to the end of a file.

    new FileWriter(file,true);

## FileWriter – Append file example

A text file with the following content:

E:\\test\\filename.txt

    ABC Hello

Java example to append new content to the end of a file.

AppendToFileExample.java

    package com.mkyong;

    import java.io.BufferedWriter;
    import java.io.File;
    import java.io.FileWriter;
    import java.io.IOException;

    public class AppendToFileExample {

    	private static final String FILENAME = "E:\\test\\filename.txt";

    	public static void main(String[] args) {

    		BufferedWriter bw = null;
    		FileWriter fw = null;

    		try {

    			String data = " This is new content";

    			File file = new File(FILENAME);

    			// if file doesnt exists, then create it
    			if (!file.exists()) {
    				file.createNewFile();
    			}

    			// true = append file
    			fw = new FileWriter(file.getAbsoluteFile(), true);
    			bw = new BufferedWriter(fw);

    			bw.write(data);

    			System.out.println("Done");

    		} catch (IOException e) {

    			e.printStackTrace();

    		} finally {

    			try {

    				if (bw != null)
    					bw.close();

    				if (fw != null)
    					fw.close();

    			} catch (IOException ex) {

    				ex.printStackTrace();

    			}
    		}

    	}

    }

Output: The new content is appended to the end of the file.

E:\\test\\filename.txt

    ABC Hello This is new content

## Reference

1.  [FileWriter JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/io/FileWriter.html)
2.  [BufferedWriter JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedWriter.html)
3.  [How to write to file in Java – BufferedWriter](https://www.mkyong.com/java/how-to-write-to-file-in-java-bufferedwriter-example/)

[http://www.mkyong.com/java/how-to-append-content-to-file-in-java/](http://www.mkyong.com/java/how-to-append-content-to-file-in-java/)
