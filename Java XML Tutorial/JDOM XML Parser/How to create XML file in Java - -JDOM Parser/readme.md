In this example, we show you how to use **JDOM parser** to create document, element and attribute in a XML file.

## 1\. XML File

At the end of this example, following XML file will be created.

_File : file.xml_

    <?xml version="1.0" encoding="UTF-8"?>
    <company>
      <staff id="1">
        <firstname>yong</firstname>
        <lastname>mook kim</lastname>
        <nickname>mkyong</nickname>
        <salary>199999</salary>
      </staff>
      <staff id="2">
        <firstname>low</firstname>
        <lastname>yin fong</lastname>
        <nickname>fong fong</nickname>
        <salary>188888</salary>
      </staff>
    </company>

## 3\. JDOM Example

JDOM example to create above XML file.

    import java.io.FileWriter;
    import java.io.IOException;
    import org.jdom.Attribute;
    import org.jdom.Document;
    import org.jdom.Element;
    import org.jdom.output.Format;
    import org.jdom.output.XMLOutputter;

    public class WriteXMLFile {
    	public static void main(String[] args) {

    	  try {

    		Element company = new Element("company");
    		Document doc = new Document(company);
    		doc.setRootElement(company);

    		Element staff = new Element("staff");
    		staff.setAttribute(new Attribute("id", "1"));
    		staff.addContent(new Element("firstname").setText("yong"));
    		staff.addContent(new Element("lastname").setText("mook kim"));
    		staff.addContent(new Element("nickname").setText("mkyong"));
    		staff.addContent(new Element("salary").setText("199999"));

    		doc.getRootElement().addContent(staff);

    		Element staff2 = new Element("staff");
    		staff2.setAttribute(new Attribute("id", "2"));
    		staff2.addContent(new Element("firstname").setText("low"));
    		staff2.addContent(new Element("lastname").setText("yin fong"));
    		staff2.addContent(new Element("nickname").setText("fong fong"));
    		staff2.addContent(new Element("salary").setText("188888"));

    		doc.getRootElement().addContent(staff2);

    		// new XMLOutputter().output(doc, System.out);
    		XMLOutputter xmlOutput = new XMLOutputter();

    		// display nice nice
    		xmlOutput.setFormat(Format.getPrettyFormat());
    		xmlOutput.output(doc, new FileWriter("c:\\file.xml"));

    		System.out.println("File Saved!");
    	  } catch (IOException io) {
    		System.out.println(io.getMessage());
    	  }
    	}
    }

[http://www.mkyong.com/java/how-to-create-xml-file-in-java-jdom-parser/](http://www.mkyong.com/java/how-to-create-xml-file-in-java-jdom-parser/)
