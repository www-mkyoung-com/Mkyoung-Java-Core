[Jackson](http://jackson.codehaus.org/) supports read and write JSON via high-performance **Jackson Streaming APIs**, or incremental mode. Read this Jackson [Streaming APIs](http://wiki.fasterxml.com/JacksonStreamingApi) document for detail explanation on the benefit of using streaming API.

Jackson’s streaming processing is high-performance, fast and convenient, but it’s also difficult to use, because you need to handle each and every detail of JSON data.

In this tutorial, we show you how to use following Jackson streaming APIs to read and write JSON data.

1.  `JsonGenerator` – Write to JSON.
2.  `JsonParser` – Parse JSON.

## 1\. JsonGenerator

In this example, you use “**JsonGenerator**” to write JSON “field name”, “values” and “array of values” into a file name “**file.json**“. See code comments for self-explanatory.

    import java.io.File;
    import java.io.IOException;
    import org.codehaus.jackson.JsonEncoding;
    import org.codehaus.jackson.JsonFactory;
    import org.codehaus.jackson.JsonGenerationException;
    import org.codehaus.jackson.JsonGenerator;
    import org.codehaus.jackson.map.JsonMappingException;

    public class JacksonStreamExample {
       public static void main(String[] args) {

         try {

    	JsonFactory jfactory = new JsonFactory();

    	/*** write to file ***/
    	JsonGenerator jGenerator = jfactory.createJsonGenerator(new File(
    			"c:\\user.json"), JsonEncoding.UTF8);
    	jGenerator.writeStartObject(); // {

    	jGenerator.writeStringField("name", "mkyong"); // "name" : "mkyong"
    	jGenerator.writeNumberField("age", 29); // "age" : 29

    	jGenerator.writeFieldName("messages"); // "messages" :
    	jGenerator.writeStartArray(); // [

    	jGenerator.writeString("msg 1"); // "msg 1"
    	jGenerator.writeString("msg 2"); // "msg 2"
    	jGenerator.writeString("msg 3"); // "msg 3"

    	jGenerator.writeEndArray(); // ]

    	jGenerator.writeEndObject(); // }

    	jGenerator.close();

         } catch (JsonGenerationException e) {

    	e.printStackTrace();

         } catch (JsonMappingException e) {

    	e.printStackTrace();

         } catch (IOException e) {

    	e.printStackTrace();

         }

       }

    }

As result, following new file named “**file.json**” is created :

    {
    	"name":"mkyong",
    	"age":29,
    	"messages":["msg 1","msg 2","msg 3"]
    }

## 2\. JsonParser

On the other hand, use `JsonParser` to parse or read above file “**file.json**“, and display each of the values.

**Token concept**  
In streaming mode, every JSON “string” is consider as a single token, and each tokens will be processed incremental, that why we call it “incremental mode”. For example,

    {
       "name":"mkyong"
    }

1.  Token 1 = “{“
2.  Token 2 = “name”
3.  Token 3 = “mkyong”
4.  Token 4 = “}”

See full example.

    import java.io.File;
    import java.io.IOException;
    import org.codehaus.jackson.JsonFactory;
    import org.codehaus.jackson.JsonGenerationException;
    import org.codehaus.jackson.JsonParser;
    import org.codehaus.jackson.JsonToken;
    import org.codehaus.jackson.map.JsonMappingException;

    public class JacksonStreamExample {
       public static void main(String[] args) {

         try {

    	JsonFactory jfactory = new JsonFactory();

    	/*** read from file ***/
    	JsonParser jParser = jfactory.createJsonParser(new File("c:\\user.json"));

    	// loop until token equal to "}"
    	while (jParser.nextToken() != JsonToken.END_OBJECT) {

    		String fieldname = jParser.getCurrentName();
    		if ("name".equals(fieldname)) {

    		  // current token is "name",
                      // move to next, which is "name"'s value
    		  jParser.nextToken();
    		  System.out.println(jParser.getText()); // display mkyong

    		}

    		if ("age".equals(fieldname)) {

    		  // current token is "age",
                      // move to next, which is "name"'s value
    		  jParser.nextToken();
    		  System.out.println(jParser.getIntValue()); // display 29

    		}

    		if ("messages".equals(fieldname)) {

    		  jParser.nextToken(); // current token is "[", move next

    		  // messages is array, loop until token equal to "]"
    		  while (jParser.nextToken() != JsonToken.END_ARRAY) {

                         // display msg1, msg2, msg3
    		     System.out.println(jParser.getText());

    		  }

    		}

    	  }
    	  jParser.close();

         } catch (JsonGenerationException e) {

    	  e.printStackTrace();

         } catch (JsonMappingException e) {

    	  e.printStackTrace();

         } catch (IOException e) {

    	  e.printStackTrace();

         }

      }

    }

**Warning**  
The array parsing is a bit tricky, read code comments for explanation.

_Output_

    mkyong
    29
    msg 1
    msg 2
    msg 3

## Conclusion

In summary, for performance critical application, use Steaming API, otherwise, just use normal [Jackson data binding](http://www.mkyong.com/java/how-to-convert-java-object-to-from-json-jackson/).

## References

1.  [Jackson Streaming API documentation](http://wiki.fasterxml.com/JacksonStreamingApi)
2.  [Jackson Streaming API short example](http://wiki.fasterxml.com/JacksonInFiveMinutes)
3.  [Gson Streaming example](http://www.mkyong.com/java/gson-streaming-to-read-and-write-json/)

[http://www.mkyong.com/java/jackson-streaming-api-to-read-and-write-json/](http://www.mkyong.com/java/jackson-streaming-api-to-read-and-write-json/)
