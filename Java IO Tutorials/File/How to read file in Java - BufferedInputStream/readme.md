Here is another example to show how to read a file in Java with `BufferedInputStream` and `DataInputStream` classes.

The `readLine()` from the type `DataInputStream` is deprecated. Sun officially announced this method can not convert property from bytes to characters. It’s advised to use `BufferedReader`.

You may interest to read this [How to read file from Java – BufferedReader](http://www.mkyong.com/java/how-to-read-file-from-java-bufferedreader-example)

    package com.mkyong.io;

    import java.io.BufferedInputStream;
    import java.io.DataInputStream;
    import java.io.File;
    import java.io.FileInputStream;
    import java.io.IOException;

    public class BufferedInputStreamExample {

    	public static void main(String[] args) {

    		File file = new File("C:\\testing.txt");
    		FileInputStream fis = null;
    		BufferedInputStream bis = null;
    		DataInputStream dis = null;

    		try {
    			fis = new FileInputStream(file);

    			bis = new BufferedInputStream(fis);
    			dis = new DataInputStream(bis);

    			while (dis.available() != 0) {
    				System.out.println(dis.readLine());
    			}

    		} catch (IOException e) {
    			e.printStackTrace();
    		} finally {
    			try {
    				fis.close();
    				bis.close();
    				dis.close();
    			} catch (IOException ex) {
    				ex.printStackTrace();
    			}
    		}
    	}
    }

[http://www.mkyong.com/java/how-to-read-file-from-java-bufferedinputstream-example/](http://www.mkyong.com/java/how-to-read-file-from-java-bufferedinputstream-example/)
