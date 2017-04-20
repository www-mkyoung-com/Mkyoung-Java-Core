**JAXB**, stands for **Java Architecture for XML Binding**, using JAXB annotation to convert Java object to / from XML file. In this tutorial, we show you how to use JAXB to do following stuffs :

1.  Marshalling – Convert a Java object into a XML file.
2.  Unmarshalling – Convert XML content into a Java Object.

Technologies used in this article

1.  JDK 1.6
2.  JAXB 2.0

Working with JAXB is easy, just annotate object with JAXB annotation, later use `jaxbMarshaller.marshal()` or `jaxbMarshaller.unmarshal()` to do the object / XML conversion.

## 1\. JAXB Dependency

No extra jaxb libraries are required if you are using JDK1.6 or above, because [JAXB is bundled in JDK 1.6](http://jaxb.java.net/guide/Which_JAXB_RI_is_included_in_which_JDK_.html).

Note  
For JDK < 1.6, download JAXB from [here](http://jaxb.java.net/), and puts “**jaxb-api.jar**” and “**jaxb-impl.jar**” on your project classpath.

## 2\. JAXB Annotation

For object that need to convert to / from XML file, it have to annotate with JAXB annotation. The annotation are pretty self-explanatory, you can refer to this [JAXB guide](http://jaxb.java.net/tutorial/) for detail explanation.

    package com.mkyong.core;

    import javax.xml.bind.annotation.XmlAttribute;
    import javax.xml.bind.annotation.XmlElement;
    import javax.xml.bind.annotation.XmlRootElement;

    @XmlRootElement
    public class Customer {

    	String name;
    	int age;
    	int id;

    	public String getName() {
    		return name;
    	}

    	@XmlElement
    	public void setName(String name) {
    		this.name = name;
    	}

    	public int getAge() {
    		return age;
    	}

    	@XmlElement
    	public void setAge(int age) {
    		this.age = age;
    	}

    	public int getId() {
    		return id;
    	}

    	@XmlAttribute
    	public void setId(int id) {
    		this.id = id;
    	}

    }

## 3\. Convert Object to XML

JAXB marshalling example, convert customer object into a XML file. The `jaxbMarshaller.marshal()` contains a lot of overloaded methods, find one that suit your output.

    package com.mkyong.core;

    import java.io.File;
    import javax.xml.bind.JAXBContext;
    import javax.xml.bind.JAXBException;
    import javax.xml.bind.Marshaller;

    public class JAXBExample {
    	public static void main(String[] args) {

    	  Customer customer = new Customer();
    	  customer.setId(100);
    	  customer.setName("mkyong");
    	  customer.setAge(29);

    	  try {

    		File file = new File("C:\\file.xml");
    		JAXBContext jaxbContext = JAXBContext.newInstance(Customer.class);
    		Marshaller jaxbMarshaller = jaxbContext.createMarshaller();

    		// output pretty printed
    		jaxbMarshaller.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);

    		jaxbMarshaller.marshal(customer, file);
    		jaxbMarshaller.marshal(customer, System.out);

    	      } catch (JAXBException e) {
    		e.printStackTrace();
    	      }

    	}
    }

_Output_

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <customer id="100">
        <age>29</age>
        <name>mkyong</name>
    </customer>

## 4\. Convert XML to Object

JAXB unmarshalling example, convert a XML file content into a customer object. The `jaxbMarshaller.unmarshal()`contains a lot of overloaded methods, find one that suit yours.

    package com.mkyong.core;

    import java.io.File;
    import javax.xml.bind.JAXBContext;
    import javax.xml.bind.JAXBException;
    import javax.xml.bind.Unmarshaller;

    public class JAXBExample {
    	public static void main(String[] args) {

    	 try {

    		File file = new File("C:\\file.xml");
    		JAXBContext jaxbContext = JAXBContext.newInstance(Customer.class);

    		Unmarshaller jaxbUnmarshaller = jaxbContext.createUnmarshaller();
    		Customer customer = (Customer) jaxbUnmarshaller.unmarshal(file);
    		System.out.println(customer);

    	  } catch (JAXBException e) {
    		e.printStackTrace();
    	  }

    	}
    }

_Output_

    Customer [name=mkyong, age=29, id=100]

[http://www.mkyong.com/java/jaxb-hello-world-example/](http://www.mkyong.com/java/jaxb-hello-world-example/)
