
In this tutorial, we will show you how to use [Gson](https://github.com/google/gson) to convert Java object to / from JSON.

_P.S All examples are tested with Gson 2.6.2_

**Note**  
JSON stands for JavaScript Object Notation, it is a lightweight data-interchange format. You can see many Java applications started to throw away XML format and start using JSON as a new data-interchange format. Java is all about object, often times, you need to convert an object into JSON format for data-interchange or vice verse.

**Note**  
Jackson is another high performance JSON processor, try this [Jackson 2 – Java object to / from JSON](http://www.mkyong.com/java/jackson-2-convert-java-object-to-from-json/)

## 1\. Quick Reference

1.1 `toJson()` – Convert Java object to JSON

    Gson gson = new Gson();
    Staff obj = new Staff();

    // 1\. Java object to JSON, and save into a file
    gson.toJson(obj, new FileWriter("D:\\file.json"));

    // 2\. Java object to JSON, and assign to a String
    String jsonInString = gson.toJson(obj);

1.2 `fromJson()` – Convert JSON to Java object

    Gson gson = new Gson();

    // 1\. JSON to Java object, read it from a file.
    Staff staff = gson.fromJson(new FileReader("D:\\file.json"), Staff.class);

    // 2\. JSON to Java object, read it from a Json String.
    String jsonInString = "{'name' : 'mkyong'}";
    Staff staff = gson.fromJson(jsonInString, Staff.class);

    // JSON to JsonElement, convert to String later.
    JsonElement json = gson.fromJson(new FileReader("D:\\file.json"), JsonElement.class);
        String result = gson.toJson(json);

## 2\. Gson Dependency

To use Gson, declares the following dependency.

pom.xml

    <dependency>
        	<groupId>com.google.code.gson</groupId>
        	<artifactId>gson</artifactId>
        	<version>2.6.2</version>
    </dependency>

## 3\. POJO

A simple POJO, for testing later.

staff.java

    package com.mkyong.json;

    import java.math.BigDecimal;
    import java.util.List;

    public class Staff {

    	private String name;
    	private int age;
    	private String position;
    	private BigDecimal salary;
    	private List<String> skills;

    	//...

## 4\. Java Object to JSON

Gson example to convert a `Staff` object into a JSON formatted string.

GsonExample.java

    package com.mkyong.json;

    import com.google.gson.Gson;

    import java.io.FileWriter;
    import java.io.IOException;
    import java.math.BigDecimal;
    import java.util.ArrayList;
    import java.util.List;

    public class GsonExample {

        public static void main(String[] args) {

            Staff staff = createDummyObject();

            //1\. Convert object to JSON string
            Gson gson = new Gson();
            String json = gson.toJson(staff);
            System.out.println(json);

            //2\. Convert object to JSON string and save into a file directly
            try (FileWriter writer = new FileWriter("D:\\staff.json")) {

                gson.toJson(staff, writer);

            } catch (IOException e) {
                e.printStackTrace();
            }

        }

        private static Staff createDummyObject() {

            Staff staff = new Staff();

            staff.setName("mkyong");
            staff.setAge(35);
            staff.setPosition("Founder");
            staff.setSalary(new BigDecimal("10000"));

            List<String> skills = new ArrayList<>();
            skills.add("java");
            skills.add("python");
            skills.add("shell");

            staff.setSkills(skills);

            return staff;

        }

    }

Output

<pre>{"name":"mkyong","age":35,"position":"Founder","salary":10000,"skills":["java","python","shell"]}

//new file is created in D:\\staff.json"
</pre>

## 5\. JSON to Java Object

Gson example to read a JSON from a file and convert it back to a Java object.

Gson2Example.java

    package com.mkyong.json;

    import com.google.gson.Gson;
    import java.io.FileReader;
    import java.io.IOException;
    import java.io.Reader;

    public class Gson2Example {

        public static void main(String[] args) {

            Gson gson = new Gson();

            try (Reader reader = new FileReader("D:\\staff.json")) {

    			// Convert JSON to Java Object
                Staff staff = gson.fromJson(reader, Staff.class);
                System.out.println(staff);

    			// Convert JSON to JsonElement, and later to String
                /*JsonElement json = gson.fromJson(reader, JsonElement.class);
                String jsonInString = gson.toJson(json);
                System.out.println(jsonInString);*/

            } catch (IOException e) {
                e.printStackTrace();
            }

        }

    }

Output

<pre>Staff{name='mkyong', age=35, position='Founder', salary=10000, skills=[java, python, shell]}
</pre>

## 6\. FAQs

Some commonly ask questions.

6.1 Convert a JSON Array to a `List`, using `TypeToken`

    String json = "[{\"name\":\"mkyong\"}, {\"name\":\"laplap\"}]";
    List<Staff> list = gson.fromJson(json, new TypeToken<List<Staff>>(){}.getType());
    list.forEach(x -> System.out.println(x));

6.2 Convert a JSON to a `Map`

    String json = "{\"name\":\"mkyong\", \"age\":33}";
    Map<String, Object> map = gson.fromJson(json, new TypeToken<Map<String, Object>>(){}.getType());
    map.forEach((x,y)-> System.out.println("key : " + x + " , value : " + y));

6.3 [Enable JSON pretty print feature in Gson](http://www.mkyong.com/java/how-to-enable-pretty-print-json-output-gson/)

## References

1.  [Google Gson](https://github.com/google/gson)
2.  [Json Official site](http://www.json.org/)
3.  [Wikipedia – Json](http://en.wikipedia.org/wiki/JSON)

[http://www.mkyong.com/java/how-do-convert-java-object-to-from-json-format-gson-api/](http://www.mkyong.com/java/how-do-convert-java-object-to-from-json-format-gson-api/)
