In this tutorial, we will show you how to read an XML file via **DOM XML parser**. DOM parser parses the entire XML document and loads it into memory; then models it in a “TREE” structure for easy traversal or manipulation.

In short, it turns a XML file into [DOM](http://www.w3schools.com/dom/default.asp) or Tree structure, and you have to traverse a node by node to get what you want.

**What is Node?**  
In the DOM, everything in an XML document is a node, [read this](http://www.w3schools.com/dom/dom_nodes.asp).

**Warning**  
DOM Parser is slow and consumes a lot of memory when it loads an XML document which contains a lot of data. Please consider SAX parser as solution for it, SAX is faster than DOM and use less memory.

## 1\. DOM XML Parser Example

This example shows you how to get the node by “name”, and display the value.

/Users/mkyong/staff.xml

    <?xml version="1.0"?>
    <company>
    	<staff id="1001">
    		<firstname>yong</firstname>
    		<lastname>mook kim</lastname>
    		<nickname>mkyong</nickname>
    		<salary>100000</salary>
    	</staff>
    	<staff id="2001">
    		<firstname>low</firstname>
    		<lastname>yin fong</lastname>
    		<nickname>fong fong</nickname>
    		<salary>200000</salary>
    	</staff>
    </company>

ReadXMLFile.java

    package com.mkyong.seo;

    import javax.xml.parsers.DocumentBuilderFactory;
    import javax.xml.parsers.DocumentBuilder;
    import org.w3c.dom.Document;
    import org.w3c.dom.NodeList;
    import org.w3c.dom.Node;
    import org.w3c.dom.Element;
    import java.io.File;

    public class ReadXMLFile {

      public static void main(String argv[]) {

        try {

    	File fXmlFile = new File("/Users/mkyong/staff.xml");
    	DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
    	DocumentBuilder dBuilder = dbFactory.newDocumentBuilder();
    	Document doc = dBuilder.parse(fXmlFile);

    	//optional, but recommended
    	//read this - http://stackoverflow.com/questions/13786607/normalization-in-dom-parsing-with-java-how-does-it-work
    	doc.getDocumentElement().normalize();

    	System.out.println("Root element :" + doc.getDocumentElement().getNodeName());

    	NodeList nList = doc.getElementsByTagName("staff");

    	System.out.println("----------------------------");

    	for (int temp = 0; temp < nList.getLength(); temp++) {

    		Node nNode = nList.item(temp);

    		System.out.println("\nCurrent Element :" + nNode.getNodeName());

    		if (nNode.getNodeType() == Node.ELEMENT_NODE) {

    			Element eElement = (Element) nNode;

    			System.out.println("Staff id : " + eElement.getAttribute("id"));
    			System.out.println("First Name : " + eElement.getElementsByTagName("firstname").item(0).getTextContent());
    			System.out.println("Last Name : " + eElement.getElementsByTagName("lastname").item(0).getTextContent());
    			System.out.println("Nick Name : " + eElement.getElementsByTagName("nickname").item(0).getTextContent());
    			System.out.println("Salary : " + eElement.getElementsByTagName("salary").item(0).getTextContent());

    		}
    	}
        } catch (Exception e) {
    	e.printStackTrace();
        }
      }

    }

Result

    Root element :company
    ----------------------------

    Current Element :staff
    Staff id : 1001
    First Name : yong
    Last Name : mook kim
    Nick Name : mkyong
    Salary : 100000

    Current Element :staff
    Staff id : 2001
    First Name : low
    Last Name : yin fong
    Nick Name : fong fong
    Salary : 200000

## 2\. Looping the Node

This example reads the same "`staff.xml`", and showing you how to loop the node one by one, and print out the node name and value, and also the attribute if any.

ReadXMLFile2.java

    package com.mkyong.seo;

    import java.io.File;
    import javax.xml.parsers.DocumentBuilder;
    import javax.xml.parsers.DocumentBuilderFactory;
    import org.w3c.dom.Document;
    import org.w3c.dom.NamedNodeMap;
    import org.w3c.dom.Node;
    import org.w3c.dom.NodeList;

    public class ReadXMLFile2 {

      public static void main(String[] args) {

        try {

    	File file = new File("/Users/mkyong/staff.xml");

    	DocumentBuilder dBuilder = DocumentBuilderFactory.newInstance()
                                 .newDocumentBuilder();

    	Document doc = dBuilder.parse(file);

    	System.out.println("Root element :" + doc.getDocumentElement().getNodeName());

    	if (doc.hasChildNodes()) {

    		printNote(doc.getChildNodes());

    	}

        } catch (Exception e) {
    	System.out.println(e.getMessage());
        }

      }

      private static void printNote(NodeList nodeList) {

        for (int count = 0; count < nodeList.getLength(); count++) {

    	Node tempNode = nodeList.item(count);

    	// make sure it's element node.
    	if (tempNode.getNodeType() == Node.ELEMENT_NODE) {

    		// get node name and value
    		System.out.println("\nNode Name =" + tempNode.getNodeName() + " [OPEN]");
    		System.out.println("Node Value =" + tempNode.getTextContent());

    		if (tempNode.hasAttributes()) {

    			// get attributes names and values
    			NamedNodeMap nodeMap = tempNode.getAttributes();

    			for (int i = 0; i < nodeMap.getLength(); i++) {

    				Node node = nodeMap.item(i);
    				System.out.println("attr name : " + node.getNodeName());
    				System.out.println("attr value : " + node.getNodeValue());

    			}

    		}

    		if (tempNode.hasChildNodes()) {

    			// loop again if has child nodes
    			printNote(tempNode.getChildNodes());

    		}

    		System.out.println("Node Name =" + tempNode.getNodeName() + " [CLOSE]");

    	}

        }

      }

    }

Result :

    Root element :company

    Node Name =company [OPEN]
    Node Value =

    		yong
    		mook kim
    		mkyong
    		100000

    		low
    		yin fong
    		fong fong
    		200000

    Node Name =staff [OPEN]
    Node Value =
    		yong
    		mook kim
    		mkyong
    		100000

    attr name : id
    attr value : 1001

    Node Name =firstname [OPEN]
    Node Value =yong
    Node Name =firstname [CLOSE]

    Node Name =lastname [OPEN]
    Node Value =mook kim
    Node Name =lastname [CLOSE]

    Node Name =nickname [OPEN]
    Node Value =mkyong
    Node Name =nickname [CLOSE]

    Node Name =salary [OPEN]
    Node Value =100000
    Node Name =salary [CLOSE]
    Node Name =staff [CLOSE]

    Node Name =staff [OPEN]
    Node Value =
    		low
    		yin fong
    		fong fong
    		200000

    attr name : id
    attr value : 2001

    Node Name =firstname [OPEN]
    Node Value =low
    Node Name =firstname [CLOSE]

    Node Name =lastname [OPEN]
    Node Value =yin fong
    Node Name =lastname [CLOSE]

    Node Name =nickname [OPEN]
    Node Value =fong fong
    Node Name =nickname [CLOSE]

    Node Name =salary [OPEN]
    Node Value =200000
    Node Name =salary [CLOSE]
    Node Name =staff [CLOSE]
    Node Name =company [CLOSE]

**Note**  
You may interest at this [How to get Alexa Ranking In Java](http://www.mkyong.com/java/how-to-get-alexa-ranking-in-java/). It shows you how to use DOM to parse the Alexa XML result.

## References

1.  [When to Use DOM](http://docs.oracle.com/javase/tutorial/jaxp/dom/when.html)
2.  [Normalization in DOM parsing with java - how does it work?](http://stackoverflow.com/questions/13786607/normalization-in-dom-parsing-with-java-how-does-it-work)
3.  [Learn XML DOM](http://www.w3schools.com/dom/default.asp)
4.  [What is Node?](http://www.w3schools.com/dom/dom_nodes.asp)
5.  [What is Element?](http://www.w3schools.com/dom/dom_element.asp)

[http://www.mkyong.com/java/how-to-read-xml-file-in-java-dom-parser/](http://www.mkyong.com/java/how-to-read-xml-file-in-java-dom-parser/)
