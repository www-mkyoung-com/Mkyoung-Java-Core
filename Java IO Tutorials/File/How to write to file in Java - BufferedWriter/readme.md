In Java, you can use `java.io.BufferedWriter` to write content to a file.

**Note**  
The `BufferedWriter` is a character stream class to handle the character data. Unlike byte stream (convert data into bytes), you can just write the strings, arrays or character data directly to a file.

## 1\. Classic BufferedWriter

A classic `BufferedWriter` example to write content to a file, create the file if doesn’t exist, the existing content will be overridden.

WriteToFileExample1.java

    package com.mkyong;

    import java.io.BufferedWriter;
    import java.io.FileWriter;
    import java.io.IOException;

    public class WriteToFileExample1 {

    	private static final String FILENAME = "E:\\test\\filename.txt";

    	public static void main(String[] args) {

    		BufferedWriter bw = null;
    		FileWriter fw = null;

    		try {

    			String content = "This is the content to write into file\n";

    			fw = new FileWriter(FILENAME);
    			bw = new BufferedWriter(fw);
    			bw.write(content);

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

Output : A new file is created with the following content :

E:\\test\\filename.txt

    This is the content to write into file

## 2\. JDK7 Example

`try-with-resources` example to auto close the file writer.

WriteToFileExample2.java

    package com.mkyong;

    import java.io.BufferedWriter;
    import java.io.FileWriter;
    import java.io.IOException;

    public class WriteToFileExample2 {

    	private static final String FILENAME = "E:\\test\\filename.txt";

    	public static void main(String[] args) {

    		try (BufferedWriter bw = new BufferedWriter(new FileWriter(FILENAME))) {

    			String content = "This is the content to write into file\n";

    			bw.write(content);

    			// no need to close it.
    			//bw.close();

    			System.out.println("Done");

    		} catch (IOException e) {

    			e.printStackTrace();

    		}

    	}

    }

## 3\. BufferedWriter – Append

To append content to the end of a file, pass a `true` to `FileWriter`

    // append to end of file
    FileWriter fw = new FileWriter(FILENAME, true);
    BufferedWriter bw = new BufferedWriter(fw);

## References

1.  [The try-with-resources Statement](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html)
2.  [How to append content to file in Java](https://www.mkyong.com/java/how-to-append-content-to-file-in-java/)
3.  [BufferedWriter JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedWriter.html)

[http://www.mkyong.com/java/how-to-write-to-file-in-java-bufferedwriter-example/](http://www.mkyong.com/java/how-to-write-to-file-in-java-bufferedwriter-example/)
