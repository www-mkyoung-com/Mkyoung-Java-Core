In Java, [FileOutputStream](http://docs.oracle.com/javase/1.4.2/docs/api/java/io/FileOutputStream.html) is a bytes stream class that’s used to handle raw binary data. To write the data to file, you have to convert the data into bytes and save it to file. See below full example.

    package com.mkyong.io;

    import java.io.File;
    import java.io.FileOutputStream;
    import java.io.IOException;

    public class WriteFileExample {
    	public static void main(String[] args) {

    		FileOutputStream fop = null;
    		File file;
    		String content = "This is the text content";

    		try {

    			file = new File("c:/newfile.txt");
    			fop = new FileOutputStream(file);

    			// if file doesnt exists, then create it
    			if (!file.exists()) {
    				file.createNewFile();
    			}

    			// get the content in bytes
    			byte[] contentInBytes = content.getBytes();

    			fop.write(contentInBytes);
    			fop.flush();
    			fop.close();

    			System.out.println("Done");

    		} catch (IOException e) {
    			e.printStackTrace();
    		} finally {
    			try {
    				if (fop != null) {
    					fop.close();
    				}
    			} catch (IOException e) {
    				e.printStackTrace();
    			}
    		}
    	}
    }

An updated JDK7 example, using new “try resource close” method to handle file easily.

    package com.mkyong.io;

    import java.io.File;
    import java.io.FileOutputStream;
    import java.io.IOException;

    public class WriteFileExample {
    	public static void main(String[] args) {

    		File file = new File("c:/newfile.txt");
    		String content = "This is the text content";

    		try (FileOutputStream fop = new FileOutputStream(file)) {

    			// if file doesn't exists, then create it
    			if (!file.exists()) {
    				file.createNewFile();
    			}

    			// get the content in bytes
    			byte[] contentInBytes = content.getBytes();

    			fop.write(contentInBytes);
    			fop.flush();
    			fop.close();

    			System.out.println("Done");

    		} catch (IOException e) {
    			e.printStackTrace();
    		}
    	}
    }

## References

1.  [http://java.sun.com/j2se/1.4.2/docs/api/java/io/FileOutputStream.html](http://java.sun.com/j2se/1.4.2/docs/api/java/io/FileOutputStream.html)
2.  [http://www.mkyong.com/java/how-to-read-file-in-java-fileinputstream/](http://www.mkyong.com/java/how-to-read-file-in-java-fileinputstream/)

[http://www.mkyong.com/java/how-to-write-to-file-in-java-fileoutputstream-example/](http://www.mkyong.com/java/how-to-write-to-file-in-java-fileoutputstream-example/)
