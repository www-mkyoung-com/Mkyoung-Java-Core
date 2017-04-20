**JDOM XML parser** example to modify an existing XML file :

1.  Add a new element
2.  Update existing element attribute
3.  Update existing element value
4.  Delete existing element

## 1\. XML File

See before and after XML file.

_File : file.xml_ – Original XML file.

    <?xml version="1.0" encoding="UTF-8"?>
    <company>
      <staff id="1">
        <firstname>yong</firstname>
        <lastname>mook kim</lastname>
        <nickname>mkyong</nickname>
        <salary>5000</salary>
      </staff>
    </company>

Later, update above XML file via JDOM XML Parser.

1.  Add a new “age” element under staff
2.  Update the staff attribute id = 2
3.  Update salary value to 7000
4.  Delete “firstname” element under staff

_File : file.xml_ – Newly modified XML file.

    <?xml version="1.0" encoding="UTF-8"?>
    <company>
      <staff id="2">
        <lastname>mook kim</lastname>
        <nickname>mkyong</nickname>
        <salary>7000</salary>
        <age>28</age>
      </staff>
    </company>

## 2\. JDOM Example

JDOM parser to update or modify an existing XML file.

    import java.io.File;
    import java.io.FileWriter;
    import java.io.IOException;
    import org.jdom.Document;
    import org.jdom.Element;
    import org.jdom.JDOMException;
    import org.jdom.input.SAXBuilder;
    import org.jdom.output.Format;
    import org.jdom.output.XMLOutputter;

    public class ModifyXMLFile {
    	public static void main(String[] args) {

    	  try {

    		SAXBuilder builder = new SAXBuilder();
    		File xmlFile = new File("c:\\file.xml");

    		Document doc = (Document) builder.build(xmlFile);
    		Element rootNode = doc.getRootElement();

    		// update staff id attribute
    		Element staff = rootNode.getChild("staff");
    		staff.getAttribute("id").setValue("2");

    		// add new age element
    		Element age = new Element("age").setText("28");
    		staff.addContent(age);

    		// update salary value
    		staff.getChild("salary").setText("7000");

    		// remove firstname element
    		staff.removeChild("firstname");

    		XMLOutputter xmlOutput = new XMLOutputter();

    		// display nice nice
    		xmlOutput.setFormat(Format.getPrettyFormat());
    		xmlOutput.output(doc, new FileWriter("c:\\file.xml"));

    		// xmlOutput.output(doc, System.out);

    		System.out.println("File updated!");
    	  } catch (IOException io) {
    		io.printStackTrace();
    	  } catch (JDOMException e) {
    		e.printStackTrace();
    	  }
    	}
    }

[http://www.mkyong.com/java/how-to-modify-xml-file-in-java-jdom/](http://www.mkyong.com/java/how-to-modify-xml-file-in-java-jdom/)
