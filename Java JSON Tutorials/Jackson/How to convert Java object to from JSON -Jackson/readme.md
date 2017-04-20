In this tutorial, we show you how to use Jackson 1.x data binding to convert Java object to / from JSON.

**Note**  
Jackson 1.x is a maintenance project, please use [Jackson 2.x](https://github.com/FasterXML/jackson) instead.

**Note**  
This tutorial is obsolete, no more update, please refer to the latest [Jackson 2 tutorial – Object to / from JSON](http://www.mkyong.com/java/jackson-2-convert-java-object-to-from-json/).

## 1\. Quick Reference

1.1 Convert Java object to JSON, `writeValue(...)`

    ObjectMapper mapper = new ObjectMapper();
    User user = new User();

    //Object to JSON in file
    mapper.writeValue(new File("c:\\user.json"), user);

    //Object to JSON in String
    String jsonInString = mapper.writeValueAsString(user);

1.2 Convert JSON to Java object, `readValue(...)`

    ObjectMapper mapper = new ObjectMapper();
    String jsonInString = "{'name' : 'mkyong'}";

    //JSON from file to Object
    User user = mapper.readValue(new File("c:\\user.json"), User.class);

    //JSON from String to Object
    User user = mapper.readValue(jsonInString, User.class);

_P.S All examples are tested with Jackson 1.9.13_

## 2\. Jackson Dependency

For Jackson 1.x, it contains 6 separate jars for different purpose, in most cases, you just need `jackson-mapper-asl`.

pom.xml

    <dependency>
    	<groupId>org.codehaus.jackson</groupId>
    	<artifactId>jackson-mapper-asl</artifactId>
    	<version>1.9.13</version>
    </dependency>

## 3\. POJO (Plain Old Java Object)

An User object for testing.

User.java

    package com.mkyong.json;

    import java.util.List;

    public class User {

    	private String name;
    	private int age;
    	private List<String> messages;

    	//getters and setters
    }

## 4\. Java Object to JSON

Convert an `user` object into a JSON formatted string.

JacksonExample.java

    package com.mkyong.json;

    import java.io.File;
    import java.io.IOException;
    import java.util.ArrayList;
    import java.util.List;

    import org.codehaus.jackson.JsonGenerationException;
    import org.codehaus.jackson.map.JsonMappingException;
    import org.codehaus.jackson.map.ObjectMapper;

    public class JacksonExample {
    	public static void main(String[] args) {

    		ObjectMapper mapper = new ObjectMapper();

    		//For testing
    		User user = createDummyUser();

    		try {
    			//Convert object to JSON string and save into file directly
    			mapper.writeValue(new File("D:\\user.json"), user);

    			//Convert object to JSON string
    			String jsonInString = mapper.writeValueAsString(user);
    			System.out.println(jsonInString);

    			//Convert object to JSON string and pretty print
    			jsonInString = mapper.writerWithDefaultPrettyPrinter().writeValueAsString(user);
    			System.out.println(jsonInString);

    		} catch (JsonGenerationException e) {
    			e.printStackTrace();
    		} catch (JsonMappingException e) {
    			e.printStackTrace();
    		} catch (IOException e) {
    			e.printStackTrace();
    		}

    	}

    	private static User createDummyUser(){

    		User user = new User();

    		user.setName("mkyong");
    		user.setAge(33);

    		List<String> msg = new ArrayList<>();
    		msg.add("hello jackson 1");
    		msg.add("hello jackson 2");
    		msg.add("hello jackson 3");

    		user.setMessages(msg);

    		return user;

    	}
    }

Output

    //new json file is created in D:\\user.json"

    {"name":"mkyong","age":33,"messages":["hello jackson 1","hello jackson 2","hello jackson 3"]}

    {
      "name" : "mkyong",
      "age" : 33,
      "messages" : [ "hello jackson 1", "hello jackson 2", "hello jackson 3" ]
    }

## 5\. JSON to Java Object

Read JSON string and convert it back to a Java object.

JacksonExample.java

    package com.mkyong.json;

    import java.io.File;
    import java.io.IOException;
    import java.util.ArrayList;
    import java.util.List;

    import org.codehaus.jackson.JsonGenerationException;
    import org.codehaus.jackson.map.JsonMappingException;
    import org.codehaus.jackson.map.ObjectMapper;

    public class JacksonExample {
    	public static void main(String[] args) {

    		ObjectMapper mapper = new ObjectMapper();

    		try {

    			// Convert JSON string from file to Object
    			User user = mapper.readValue(new File("G:\\user.json"), User.class);
    			System.out.println(user);

    			// Convert JSON string to Object
    			String jsonInString = "{\"age\":33,\"messages\":[\"msg 1\",\"msg 2\"],\"name\":\"mkyong\"}";
    			User user1 = mapper.readValue(jsonInString, User.class);
    			System.out.println(user1);

    		} catch (JsonGenerationException e) {
    			e.printStackTrace();
    		} catch (JsonMappingException e) {
    			e.printStackTrace();
    		} catch (IOException e) {
    			e.printStackTrace();
    		}

    	}

    }

Output

    User [name=mkyong, age=33, messages=[hello jackson 1, hello jackson 2, hello jackson 3]]

    User [name=mkyong, age=33, messages=[msg 1, msg 2]]

## 6\. @JsonView

`@JsonView` has been supported in Jackson since version 1.4, it lets you control what fields to display.

6.1 A simple class.

Views.java

    package com.mkyong.json;

    public class Views {

    	public static class NameOnly{};
    	public static class AgeAndName extends NameOnly{};

    }

6.2 Annotate on the fields you want to display.

User.java

    package com.mkyong.json;

    import java.util.List;
    import org.codehaus.jackson.map.annotate.JsonView;

    public class User {

    	@JsonView(Views.NameOnly.class)
    	private String name;

    	@JsonView(Views.AgeAndName.class)
    	private int age;

    	private List<String> messages;

    	//getter and setters
    }

6.3 Enable the `@JsonView` via `writerWithView()`.

JacksonExample.java

    package com.mkyong.json;

    import java.io.IOException;
    import java.util.ArrayList;
    import java.util.List;

    import org.codehaus.jackson.JsonGenerationException;
    import org.codehaus.jackson.map.JsonMappingException;
    import org.codehaus.jackson.map.ObjectMapper;
    import org.codehaus.jackson.map.SerializationConfig;

    public class JacksonExample {
    	public static void main(String[] args) {

    		ObjectMapper mapper = new ObjectMapper();
    		//By default all fields without explicit view definition are included, disable this
    		mapper.configure(SerializationConfig.Feature.DEFAULT_VIEW_INCLUSION, false);

    		//For testing
    		User user = createDummyUser();

    		try {
    			//display name only
    			String jsonInString = mapper.writerWithView(Views.NameOnly.class).writeValueAsString(user);
    			System.out.println(jsonInString);

    			//display namd ana age
    			jsonInString = mapper.writerWithView(Views.AgeAndName.class).writeValueAsString(user);
    			System.out.println(jsonInString);

    		} catch (JsonGenerationException e) {
    			e.printStackTrace();
    		} catch (JsonMappingException e) {
    			e.printStackTrace();
    		} catch (IOException e) {
    			e.printStackTrace();
    		}

    	}

    	private static User createDummyUser(){

    		User user = new User();

    		user.setName("mkyong");
    		user.setAge(33);

    		List<String> msg = new ArrayList<>();
    		msg.add("hello jackson 1");
    		msg.add("hello jackson 2");
    		msg.add("hello jackson 3");

    		user.setMessages(msg);

    		return user;

    	}
    }

Output

    {"name":"mkyong"}
    {"name":"mkyong","age":33}

## References

1.  [Jackson Project Home @github](https://github.com/FasterXML/jackson%22)
2.  [Gson – Convert Java object to / from JSON](http://www.mkyong.com/java/how-do-convert-java-object-to-from-json-format-gson-api/)

[http://www.mkyong.com/java/how-to-convert-java-object-to-from-json-jackson/](http://www.mkyong.com/java/how-to-convert-java-object-to-from-json-jackson/)
