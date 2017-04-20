Since [Gson](http://sites.google.com/site/gson/Home) version 1.6, two new classes – `JsonReader` and `JsonWriter`, are introduce to provide streaming processing on JSON data. Read this [Gson streaming documentation](http://sites.google.com/site/gson/streaming) to understand what are the benefits of using it.

Here we show you two full examples of using following Gson streaming APIs to read and write JSON data.

1.  `JsonWriter` – Streaming write to JSON.
2.  `JsonReader` – Streaming read from JSON.

Gson streaming processing is fast, but difficult to code, because you need to handle each and every detail of processing JSON data.

## 1\. JsonWriter

In this example, you use “`JsonWriter`” to write JSON data into a file name “**file.json**“. See comments for self-expalantory.

    import java.io.FileWriter;
    import java.io.IOException;
    import com.google.gson.stream.JsonWriter;

    public class GsonStreamExample {
       public static void main(String[] args) {

         JsonWriter writer;
         try {
    	writer = new JsonWriter(new FileWriter("c:\\user.json"));

    	writer.beginObject(); // {
    	writer.name("name").value("mkyong"); // "name" : "mkyong"
    	writer.name("age").value(29); // "age" : 29

    	writer.name("messages"); // "messages" :
    	writer.beginArray(); // [
    	writer.value("msg 1"); // "msg 1"
    	writer.value("msg 2"); // "msg 2"
    	writer.value("msg 3"); // "msg 3"
    	writer.endArray(); // ]

    	writer.endObject(); // }
    	writer.close();

    	System.out.println("Done");

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

## 2\. JsonReader

Example to use “`JsonReader`” to parse or read above file “file.json”.

**Token**  
In streaming mode, every JSON “data” is consider as an individual token. When you use `JsonReader` to process it, each tokens will be processed sequential.

For example,

    {
    	"url":"www.mkyong.com"
    }

Token 1 = “{”  
Token 2 = “url”  
Token 3 = “www.mkyong.com”  
Token 4 = “}”

As result, you need to keep calling “**next******” method to move to next token manually.

See full example.

    package com.mkyong.core;

    import java.io.FileNotFoundException;
    import java.io.FileReader;
    import java.io.IOException;
    import com.google.gson.stream.JsonReader;

    public class GsonStreamExample {
       public static void main(String[] args) {

         try {
    	JsonReader reader = new JsonReader(new FileReader("c:\\user.json"));

    	reader.beginObject();

    	while (reader.hasNext()) {

    	  String name = reader.nextName();

    	  if (name.equals("name")) {

    		System.out.println(reader.nextString());

    	  } else if (name.equals("age")) {

    		System.out.println(reader.nextInt());

    	  } else if (name.equals("message")) {

    		// read array
    		reader.beginArray();

    		while (reader.hasNext()) {
    			System.out.println(reader.nextString());
    		}

    		reader.endArray();

    	  } else {
    		reader.skipValue(); //avoid some unhandle events
    	  }
            }

    	reader.endObject();
    	reader.close();

         } catch (FileNotFoundException e) {
    	e.printStackTrace();
         } catch (IOException e) {
    	e.printStackTrace();
         }

       }

    }

_Output_

    mkyong
    29
    msg 1
    msg 2
    msg 3

## References

1.  [Gson streaming documentation](http://sites.google.com/site/gson/streaming)
2.  [Jackson streaming example](http://www.mkyong.com/java/jackson-streaming-api-to-read-and-write-json/)

[http://www.mkyong.com/java/gson-streaming-to-read-and-write-json/](http://www.mkyong.com/java/gson-streaming-to-read-and-write-json/)
