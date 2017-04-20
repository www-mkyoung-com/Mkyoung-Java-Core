Many developers may not aware of this function, actually, the **java.util.Properties** class come with a `storeToXML()` method to convert existing properties data into a XML file.

**Note**  
Please refer to this [Properties JavaDoc](http://download.oracle.com/javase/1.5.0/docs/api/java/util/Properties.html) for detail explanation.

    import java.io.FileOutputStream;
    import java.io.IOException;
    import java.io.OutputStream;
    import java.util.Properties;

    public class PropertiesXMLExample
    {
        public static void main(String[] args) throws IOException
        {
        	Properties props = new Properties();
        	props.setProperty("email.support", "donot-spam-me@nospam.com");

        	//where to store?
        	OutputStream os = new FileOutputStream("c:/email-configuration.xml");

        	//store the properties detail into a pre-defined XML file
        	props.storeToXML(os, "Support Email","UTF-8");

        	System.out.println("Done");
        }
    }

The above example will write the properties detail into a XML file “_c:/email-configuration.xml_“.

    <?xml version="1.0" encoding="UTF-8" standalone="no"?>
    <!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">
    	<properties>
    		<comment>Support Email</comment>
    		<entry key="email.support">donot-spam-me@nospam.com</entry>
    	</properties>

[http://www.mkyong.com/java/how-to-store-properties-into-xml-file/](http://www.mkyong.com/java/how-to-store-properties-into-xml-file/)
