DOM provides many handy classes to create XML file easily. Firstly, you have to create a Document with **DocumentBuilder** class, define all the XML content – node, attribute with **Element** class. In last, use **Transformer** class to output the entire XML content to stream output, typically a File.

In this tutorial, we show you how to use DOM XML parser to create a XML file.

## DOM Parser Example

At the end of the example, following XML file named “file.xml” will be created.

    <?xml version="1.0" encoding="UTF-8" standalone="no" ?>
    <company>
    	<staff id="1">
    		<firstname>yong</firstname>
    		<lastname>mook kim</lastname>
    		<nickname>mkyong</nickname>
    		<salary>100000</salary>
    	</staff>
    </company>

_File : WriteXMLFile.java_ – Java class to create a XML file.

    package com.mkyong.core;

    import java.io.File;
    import javax.xml.parsers.DocumentBuilder;
    import javax.xml.parsers.DocumentBuilderFactory;
    import javax.xml.parsers.ParserConfigurationException;
    import javax.xml.transform.Transformer;
    import javax.xml.transform.TransformerException;
    import javax.xml.transform.TransformerFactory;
    import javax.xml.transform.dom.DOMSource;
    import javax.xml.transform.stream.StreamResult;

    import org.w3c.dom.Attr;
    import org.w3c.dom.Document;
    import org.w3c.dom.Element;

    public class WriteXMLFile {

    	public static void main(String argv[]) {

    	  try {

    		DocumentBuilderFactory docFactory = DocumentBuilderFactory.newInstance();
    		DocumentBuilder docBuilder = docFactory.newDocumentBuilder();

    		// root elements
    		Document doc = docBuilder.newDocument();
    		Element rootElement = doc.createElement("company");
    		doc.appendChild(rootElement);

    		// staff elements
    		Element staff = doc.createElement("Staff");
    		rootElement.appendChild(staff);

    		// set attribute to staff element
    		Attr attr = doc.createAttribute("id");
    		attr.setValue("1");
    		staff.setAttributeNode(attr);

    		// shorten way
    		// staff.setAttribute("id", "1");

    		// firstname elements
    		Element firstname = doc.createElement("firstname");
    		firstname.appendChild(doc.createTextNode("yong"));
    		staff.appendChild(firstname);

    		// lastname elements
    		Element lastname = doc.createElement("lastname");
    		lastname.appendChild(doc.createTextNode("mook kim"));
    		staff.appendChild(lastname);

    		// nickname elements
    		Element nickname = doc.createElement("nickname");
    		nickname.appendChild(doc.createTextNode("mkyong"));
    		staff.appendChild(nickname);

    		// salary elements
    		Element salary = doc.createElement("salary");
    		salary.appendChild(doc.createTextNode("100000"));
    		staff.appendChild(salary);

    		// write the content into xml file
    		TransformerFactory transformerFactory = TransformerFactory.newInstance();
    		Transformer transformer = transformerFactory.newTransformer();
    		DOMSource source = new DOMSource(doc);
    		StreamResult result = new StreamResult(new File("C:\\file.xml"));

    		// Output to console for testing
    		// StreamResult result = new StreamResult(System.out);

    		transformer.transform(source, result);

    		System.out.println("File saved!");

    	  } catch (ParserConfigurationException pce) {
    		pce.printStackTrace();
    	  } catch (TransformerException tfe) {
    		tfe.printStackTrace();
    	  }
    	}
    }

A new XML file is created in “_C:\\file.xml_“, with default UTF-8 encoded.

**Note**  
For debugging, you can change the **StreamResult** to output the XML content to your console.

    StreamResult result =  new StreamResult(System.out);
    transformer.transform(source, result);

[http://www.mkyong.com/java/how-to-create-xml-file-in-java-dom/](http://www.mkyong.com/java/how-to-create-xml-file-in-java-dom/)
