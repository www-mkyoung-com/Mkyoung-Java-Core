In this tutorial, we will show you how to use Jackson library to pretty print JSON Object and String in the console and JSP page.

## 1\. Pretty Print JSON Object

Example to convert Object and print its output in JSON format.

    User user = new User();
    //...set user data

    ObjectMapper mapper = new ObjectMapper();
    System.out.println(mapper.writeValueAsString(user));

But the json output is in compact mode.

    {"age":29,"messages":["msg 1","msg 2","msg 3"],"name":"mkyong"}

To enable pretty print, use `writerWithDefaultPrettyPrinter`.

    ObjectMapper mapper = new ObjectMapper();
    System.out.println(mapper.writerWithDefaultPrettyPrinter().writeValueAsString(user));

Output

    {
      "age" : 29,
      "messages" : [ "msg 1", "msg 2", "msg 3" ],
      "name" : "mkyong"
    }

## 2\. Pretty Print JSON String

This is a bit tricky, try to use `writerWithDefaultPrettyPrinter` again.

    String test = "{\"age\":29,\"messages\":[\"msg 1\",\"msg 2\",\"msg 3\"],\"name\":\"mkyong\"}";
    System.out.println(mapper.writerWithDefaultPrettyPrinter().writeValueAsString(test));

Output, not what we want, json is still in compact mode.

    "{\"age\":29,\"messages\":[\"msg 1\",\"msg 2\",\"msg 3\"],\"name\":\"mkyong\"}"

To solve it, bind the JSON string to Object before pretty print it.

    String test = "{\"age\":29,\"messages\":[\"msg 1\",\"msg 2\",\"msg 3\"],\"name\":\"mkyong\"}";
    Object json = mapper.readValue(test, Object.class);
    System.out.println(mapper.writerWithDefaultPrettyPrinter().writeValueAsString(json));

Output

    {
      "age" : 29,
      "messages" : [ "msg 1", "msg 2", "msg 3" ],
      "name" : "mkyong"
    }

## 3\. Pretty Print JSON in JSP page

To pretty print JSON data in a JSP page or any other HTML page, just wrap the json data with `<pre>` tag. This example is using Spring MVC and JSP page.

Controller Class

    @Controller
    @RequestMapping("/anything")
    public class AdminController {

      @RequestMapping(method = RequestMethod.GET)
      public ModelAndView index() {

    	String test = "{\"age\":29,\"messages\":[\"msg 1\",\"msg 2\",\"msg 3\"],\"name\":\"mkyong\"}";
    	Object json = mapper.readValue(test, Object.class);

    	ModelAndView modelandView = new ModelAndView("viewname");

    	modelandView.addObject("output", mapper.writerWithDefaultPrettyPrinter().writeValueAsString(json));

    	return modelandViewl;

      }

    }

In html page.  
`<pre>${output}</pre>`

**Note – 12/12/2013**  
Article is updated to use `writerWithDefaultPrettyPrinter()`, the old `defaultPrettyPrintingWriter()` is deprecated.

## References

1.  [Jackson – High-performance JSON processor.](http://jackson.codehaus.org/)
2.  [ObjectMapper JavaDoc](http://jackson.codehaus.org/1.9.0/javadoc/org/codehaus/jackson/map/ObjectMapper.html)

[http://www.mkyong.com/java/how-to-enable-pretty-print-json-output-jackson/](http://www.mkyong.com/java/how-to-enable-pretty-print-json-output-jackson/)
