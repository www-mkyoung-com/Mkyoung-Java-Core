[JSON.simple](https://github.com/fangyidong/json-simple) is a simple Java library for JSON processing, read and write JSON data and full compliance with [JSON specification (RFC4627)](http://www.ietf.org/rfc/rfc4627.txt).

**Note**  
Alternatively, you should consider [Jackson 2](http://www.mkyong.com/java/jackson-2-convert-java-object-to-from-json/) or [Gson](http://www.mkyong.com/java/how-do-convert-java-object-to-from-json-format-gson-api/)

In this tutorial, we show you how to use **JSON.simple** to read and write JSON data from / to a file.

## 1\. JSON.simple Dependency

**JSON.simple** is available at Maven central repository.

pom.xml

    <dependency>
        <groupId>com.googlecode.json-simple</groupId>
        <artifactId>json-simple</artifactId>
        <version>1.1.1</version>
    </dependency>

## 2\. Write JSON to file

In below example, it writes JSON data via `JSONObject` and `JSONArray`, and save it into a file named “f:\\test.json”.

JsonSimpleWriteExample.java

    package com.mkyong;

    import org.json.simple.JSONArray;
    import org.json.simple.JSONObject;

    import java.io.FileWriter;
    import java.io.IOException;

    public class JsonSimpleWriteExample {

        public static void main(String[] args) {

            JSONObject obj = new JSONObject();
            obj.put("name", "mkyong.com");
            obj.put("age", new Integer(100));

            JSONArray list = new JSONArray();
            list.add("msg 1");
            list.add("msg 2");
            list.add("msg 3");

            obj.put("messages", list);

            try (FileWriter file = new FileWriter("f:\\test.json")) {

                file.write(obj.toJSONString());
                file.flush();

            } catch (IOException e) {
                e.printStackTrace();
            }

            System.out.print(obj);

        }

    }

Output

f:\\test.json

    {
    	"age":100,
    	"name":"mkyong.com",
    	"messages":["msg 1","msg 2","msg 3"]
    }

## 3\. Read JSON from file

Use `JSONParser` to read above generated JSON file “f:\\test.json”, and display each of the values.

JsonSimpleReadExample.java

    package com.mkyong;

    import org.json.simple.JSONArray;
    import org.json.simple.JSONObject;
    import org.json.simple.parser.JSONParser;
    import org.json.simple.parser.ParseException;

    import java.io.FileNotFoundException;
    import java.io.FileReader;
    import java.io.IOException;
    import java.util.Iterator;

    public class JsonSimpleReadExample {

        public static void main(String[] args) {

            JSONParser parser = new JSONParser();

            try {

                Object obj = parser.parse(new FileReader("f:\\test.json"));

                JSONObject jsonObject = (JSONObject) obj;
                System.out.println(jsonObject);

                String name = (String) jsonObject.get("name");
                System.out.println(name);

                long age = (Long) jsonObject.get("age");
                System.out.println(age);

                // loop array
                JSONArray msg = (JSONArray) jsonObject.get("messages");
                Iterator<String> iterator = msg.iterator();
                while (iterator.hasNext()) {
                    System.out.println(iterator.next());
                }

            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            } catch (ParseException e) {
                e.printStackTrace();
            }

        }

    }

_Output_

    {"name":"mkyong.com","messages":["msg 1","msg 2","msg 3"],"age":100}
    mkyong.com
    100
    msg 1
    msg 2
    msg 3

## References

1.  [JSON.simple official website](http://code.google.com/p/json-simple/)
2.  [JSON.simple encoding JSON example](http://code.google.com/p/json-simple/wiki/EncodingExamples)
3.  [JSON.simple decoding JSON example](http://code.google.com/p/json-simple/wiki/DecodingExamples)

[http://www.mkyong.com/java/json-simple-example-read-and-write-json/](http://www.mkyong.com/java/json-simple-example-read-and-write-json/)
