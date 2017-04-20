In last article, we show you how to [convert properties file into XML file](http://www.mkyong.com/java/how-to-store-properties-into-xml-file/). See following XML file :

    <?xml version="1.0" encoding="UTF-8" standalone="no"?>
    <!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">
       <properties>
    	<comment>Support Email</comment>
    	<entry key="email.support">donot-spam-me@nospam.com</entry>
       </properties>

In this example, we show you how to use **loadFromXML()** method to load above XML file into a properties object, and get the key “_email.support_” value via `getProperty()` method.

    package com.mkyong;

    import java.io.FileInputStream;
    import java.io.IOException;
    import java.io.InputStream;
    import java.util.Properties;

    public class PropertiesXMLExample
    {
        public static void main(String[] args) throws IOException
        {
        	Properties props = new Properties();

        	InputStream is = new FileInputStream("c:/email-configuration.xml");
        	//load the xml file into properties format
        	props.loadFromXML(is);

        	String email = props.getProperty("email.support");

        	System.out.println(email);

        }
    }

**Output**  
The above example will print out the value of properties key : “**email.support**” :

    donot-spam-me@nospam.com

[http://www.mkyong.com/java/how-to-load-properties-from-xml-file/](http://www.mkyong.com/java/how-to-load-properties-from-xml-file/)
