In Java, you can use `java.io.BufferedReader` to read content from a file.

**Note**  
There are many ways to read a file, but this `BufferedReader` is the simplest and most common-used method.

## 1\. Classic BufferedReader

A classic `BufferedReader` to read content from a file.

E:\\test\\filename.txt

    This is the content to write into file
    This is the content to write into file

ReadFileExample1.java

    package com.mkyong;

    import java.io.BufferedReader;
    import java.io.FileReader;
    import java.io.IOException;

    public class ReadFileExample1 {

    	private static final String FILENAME = "E:\\test\\filename.txt";

    	public static void main(String[] args) {

    		BufferedReader br = null;
    		FileReader fr = null;

    		try {

    			fr = new FileReader(FILENAME);
    			br = new BufferedReader(fr);

    			String sCurrentLine;

    			br = new BufferedReader(new FileReader(FILENAME));

    			while ((sCurrentLine = br.readLine()) != null) {
    				System.out.println(sCurrentLine);
    			}

    		} catch (IOException e) {

    			e.printStackTrace();

    		} finally {

    			try {

    				if (br != null)
    					br.close();

    				if (fr != null)
    					fr.close();

    			} catch (IOException ex) {

    				ex.printStackTrace();

    			}

    		}

    	}

    }

Output :

    This is the content to write into file
    This is the content to write into file

## 2\. JDK7 Example

`try-with-resources` example to auto close the file reader.

ReadFileExample2.java

    package com.mkyong;

    import java.io.BufferedReader;
    import java.io.FileReader;
    import java.io.IOException;

    public class ReadFileExample2 {

    	private static final String FILENAME = "E:\\test\\filename.txt";

    	public static void main(String[] args) {

    		try (BufferedReader br = new BufferedReader(new FileReader(FILENAME))) {

    			String sCurrentLine;

    			while ((sCurrentLine = br.readLine()) != null) {
    				System.out.println(sCurrentLine);
    			}

    		} catch (IOException e) {
    			e.printStackTrace();
    		}

    	}

    }

## References

1.  [The try-with-resources Statement](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html)
2.  [How to append content to file in Java](https://www.mkyong.com/java/how-to-append-content-to-file-in-java/)
3.  [BufferedReader JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html)
4.  [How to write to file in Java – BufferedWriter](https://www.mkyong.com/java/how-to-write-to-file-in-java-bufferedwriter-example/)

[http://www.mkyong.com/java/how-to-read-file-from-java-bufferedreader-example/](http://www.mkyong.com/java/how-to-read-file-from-java-bufferedreader-example/)
