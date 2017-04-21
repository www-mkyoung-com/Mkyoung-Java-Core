Java object can write into a file for future access, this is called [Serialization](https://en.wikipedia.org/wiki/Serialization). In order to do this, you have to implement the `Serializable`interface, and use `ObjectOutputStream` to write objects into a file.

    FileOutputStream fout = new FileOutputStream("c:\\temp\\address.ser");
    ObjectOutputStream oos = new ObjectOutputStream(fout);
    oos.writeObject(address);

## 1\. Object

Create an “Address” object and implement the `Serializable` interface. This object is going to write into a file.

Address.java

    package com.mkyong.io;

    import java.io.Serializable;

    public class Address implements Serializable {

    	private static final long serialVersionUID = 1L;

    	String street;
    	String country;

    	public void setStreet(String street) {
    		this.street = street;
    	}

    	public void setCountry(String country) {
    		this.country = country;
    	}

    	public String getStreet() {
    		return this.street;
    	}

    	public String getCountry() {
    		return this.country;
    	}

    	@Override
    	public String toString() {
    		return new StringBuffer(" Street : ")
    				.append(this.street).append(" Country : ")
    				.append(this.country).toString();
    	}

    }

## 2\. Write Object to File

This class will write the “Address” object and it’s variable value (“wall street”, “united state”) into a file named `c:\\temp\\address.ser`

WriteObject.java

    package com.mkyong.io;

    import java.io.FileOutputStream;
    import java.io.IOException;
    import java.io.ObjectOutputStream;

    public class WriteObject {

    	public static void main(String args[]) {

    		WriteObject obj = new WriteObject();

    		Address address = new Address();
    		address.setStreet("wall street");
    		address.setCountry("united state");

    		obj.serializeAddress(address);

    	}

    	public void serializeAddress(Address address) {

    		FileOutputStream fout = null;
    		ObjectOutputStream oos = null;

    		try {

    			fout = new FileOutputStream("c:\\temp\\address.ser");
    			oos = new ObjectOutputStream(fout);
    			oos.writeObject(address);

    			System.out.println("Done");

    		} catch (Exception ex) {

    			ex.printStackTrace();

    		} finally {

    			if (fout != null) {
    				try {
    					fout.close();
    				} catch (IOException e) {
    					e.printStackTrace();
    				}
    			}

    			if (oos != null) {
    				try {
    					oos.close();
    				} catch (IOException e) {
    					e.printStackTrace();
    				}
    			}

    		}
    	}

    	public void serializeAddressJDK7(Address address) {

    		try (ObjectOutputStream oos =
    				new ObjectOutputStream(new FileOutputStream("c:\\temp\\address2.ser"))) {

    			oos.writeObject(address);
    			System.out.println("Done");

    		} catch (Exception ex) {
    			ex.printStackTrace();
    		}

    	}

    }

**Note**  
Please read this article about [how to read the saved object from file – Java](http://www.mkyong.com/java/how-to-read-an-object-from-file-in-java/).

## References

1.  [ObjectOutputStream JavaDoc](https://docs.oracle.com/javase/7/docs/api/java/io/ObjectOutputStream.html)
2.  [Java Object Serialization](https://docs.oracle.com/javase/8/docs/technotes/guides/serialization/)
3.  [try-with-resources example in JDK 7](https://www.mkyong.com/java/try-with-resources-example-in-jdk-7/)

[http://www.mkyong.com/java/how-to-write-an-object-to-file-in-java/](http://www.mkyong.com/java/how-to-write-an-object-to-file-in-java/)
