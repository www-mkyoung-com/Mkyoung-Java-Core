In the previous example, you learn about [how to write an Object into a file](http://www.mkyong.com/java/how-to-write-an-object-to-file-in-java/). In this example, you will learn how to read an object from the saved file or how to deserialize the serialized file.

The deserialization process is quite similar with the serialization, you need to use `ObjectInputStream` to read the content of the file and convert it back to a Java object.

    FileInputStream fin = new FileInputStream("c:\\temp\\address.ser");
    ObjectInputStream ois = new ObjectInputStream(fin);
    address = (Address) ois.readObject();

## 1\. Read Object from File

This class will read a serialized file `c:\\temp\\address.ser` (created in [this example](http://www.mkyong.com/java/how-to-write-an-object-to-file-in-java/)), and convert it back to a “Address” object and print out the saved value.

ReadObject.java

    package com.mkyong.io;

    import java.io.FileInputStream;
    import java.io.IOException;
    import java.io.ObjectInputStream;

    public class ReadObject {

    	public static void main(String args[]) {

    		ReadObject obj = new ReadObject();

    		Address address = obj.deserialzeAddress("c:\\temp\\address.ser");

    		System.out.println(address);

    	}

    	public Address deserialzeAddress(String filename) {

    		Address address = null;

    		FileInputStream fin = null;
    		ObjectInputStream ois = null;

    		try {

    			fin = new FileInputStream(filename);
    			ois = new ObjectInputStream(fin);
    			address = (Address) ois.readObject();

    		} catch (Exception ex) {
    			ex.printStackTrace();
    		} finally {

    			if (fin != null) {
    				try {
    					fin.close();
    				} catch (IOException e) {
    					e.printStackTrace();
    				}
    			}

    			if (ois != null) {
    				try {
    					ois.close();
    				} catch (IOException e) {
    					e.printStackTrace();
    				}
    			}

    		}

    		return address;

    	}

    	public Address deserialzeAddressJDK7(String filename) {

    		Address address = null;

    		try (ObjectInputStream ois
    			= new ObjectInputStream(new FileInputStream(filename))) {

    			address = (Address) ois.readObject();

    		} catch (Exception ex) {
    			ex.printStackTrace();
    		}

    		return address;

    	}

    }

Output

    Street : wall street Country : united state

## References

1.  [ObjectOutputStream JavaDoc](https://docs.oracle.com/javase/7/docs/api/java/io/ObjectInputStream.html)
2.  [Java Object Serialization](https://docs.oracle.com/javase/8/docs/technotes/guides/serialization/)
3.  [try-with-resources example in JDK 7](https://www.mkyong.com/java/try-with-resources-example-in-jdk-7/)

[http://www.mkyong.com/java/how-to-read-an-object-from-file-in-java/](http://www.mkyong.com/java/how-to-read-an-object-from-file-in-java/)
