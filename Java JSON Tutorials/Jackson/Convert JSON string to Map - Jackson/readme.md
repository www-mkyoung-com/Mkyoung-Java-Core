In this tutorial, we will show you few Jackson examples to convert JSON string to/from a Map.

_P.S All examples are tested with Jackson 2.6.3_

## 1\. JSON string to Map

JsonMapExample.java

    package com.mkyong.json;

    import java.io.IOException;
    import java.util.HashMap;
    import java.util.Map;

    import com.fasterxml.jackson.core.JsonGenerationException;
    import com.fasterxml.jackson.core.type.TypeReference;
    import com.fasterxml.jackson.databind.JsonMappingException;
    import com.fasterxml.jackson.databind.ObjectMapper;

    public class JsonMapExample {

    	public static void main(String[] args) {

    		try {

    			ObjectMapper mapper = new ObjectMapper();
    			String json = "{\"name\":\"mkyong\", \"age\":29}";

    			Map<String, Object> map = new HashMap<String, Object>();

    			// convert JSON string to Map
    			map = mapper.readValue(json, new TypeReference<Map<String, String>>(){});

    			System.out.println(map);

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

    {name=mkyong, age=29}

## 2\. Map to JSON string

Example to convert the Map to JSON string.

MapJsonExample.java

    package com.mkyong.json;

    import java.io.IOException;
    import java.util.HashMap;
    import java.util.Map;

    import com.fasterxml.jackson.core.JsonGenerationException;
    import com.fasterxml.jackson.databind.JsonMappingException;
    import com.fasterxml.jackson.databind.ObjectMapper;

    public class MapJsonExample{

    	public static void main(String[] args) {

    		try {

    			ObjectMapper mapper = new ObjectMapper();
    			String json = "";

    			Map<String, Object> map = new HashMap<String, Object>();
    			map.put("name", "mkyong");
    			map.put("age", 29);

    			// convert map to JSON string
    			json = mapper.writeValueAsString(map);

    			System.out.println(json);

    			json = mapper.writerWithDefaultPrettyPrinter().writeValueAsString(map);

    			// pretty print
    			System.out.println(json);

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

    {"name":"mkyong","age":29}
    {
      "name" : "mkyong",
      "age" : 29
    }

## 3\. Map to JSON File

JsonMapFileExample.java

    package com.mkyong.json;

    import java.io.File;
    import java.io.IOException;
    import java.util.ArrayList;
    import java.util.HashMap;
    import java.util.List;
    import java.util.Map;

    import com.fasterxml.jackson.core.JsonGenerationException;
    import com.fasterxml.jackson.databind.JsonMappingException;
    import com.fasterxml.jackson.databind.ObjectMapper;

    public class JsonMapFileExample {

    	public static void main(String[] args) {

    		try {

    			ObjectMapper mapper = new ObjectMapper();

    			Map<String, Object> map = new HashMap<String, Object>();
    			map.put("name", "mkyong");
    			map.put("age", 29);

    			List<Object> list = new ArrayList<>();
    			list.add("msg 1");
    			list.add("msg 2");
    			list.add("msg 3");

    			map.put("messages", list);

    			// write JSON to a file
    			mapper.writeValue(new File("c:\\user.json"), map);

    		} catch (JsonGenerationException e) {
    			e.printStackTrace();
    		} catch (JsonMappingException e) {
    			e.printStackTrace();
    		} catch (IOException e) {
    			e.printStackTrace();
    		}
    	}

    }

c:\\user.json

    {"name":"mkyong","messages":["msg 1","msg 2","msg 3"],"age":29}

## 4\. JSON file to Map

JsonFileMapExample.java

    package com.mkyong.json;

    import java.io.File;
    import java.io.IOException;
    import java.util.ArrayList;
    import java.util.Map;

    import com.fasterxml.jackson.core.JsonGenerationException;
    import com.fasterxml.jackson.core.type.TypeReference;
    import com.fasterxml.jackson.databind.JsonMappingException;
    import com.fasterxml.jackson.databind.ObjectMapper;

    public class Jackson2Example {

    	public static void main(String[] args) {

    		try {

    			ObjectMapper mapper = new ObjectMapper();

    			// read JSON from a file
    			Map<String, Object> map = mapper.readValue(
    					new File("c:\\user.json"),
    					new TypeReference<Map<String, Object>>() {
    			});

    			System.out.println(map.get("name"));
    			System.out.println(map.get("age"));

    			@SuppressWarnings("unchecked")
    			ArrayList<String> list = (ArrayList<String>) map.get("messages");

    			for (String msg : list) {
    				System.out.println(msg);
    			}

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

    mkyong
    29
    msg 1
    msg 2
    msg 3

## References

1.  [Wikipedia : JSON](http://en.wikipedia.org/wiki/JSON)
2.  [Jackson – High-performance JSON processor](https://github.com/FasterXML/jackson)
3.  [Jackson 2 – Object to / from JSON](http://www.mkyong.com/java/jackson-2-convert-java-object-to-from-json/)

[http://www.mkyong.com/java/how-to-convert-java-map-to-from-json-jackson/](http://www.mkyong.com/java/how-to-convert-java-map-to-from-json-jackson/)
