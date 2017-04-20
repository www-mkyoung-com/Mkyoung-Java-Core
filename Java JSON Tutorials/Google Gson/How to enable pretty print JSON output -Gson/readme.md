In this tutorial, we will show you how to enable pretty print JSON output in [Gson](https://github.com/google/gson) framework.

1\. By default, Gson display the JSON output like the following :

    Gson gson = new Gson();
    String json = gson.toJson(someObj);
    System.out.println(json);

Output

<pre>{"name":"mkyong","age":35,"position":"Founder","salary":10000,"skills":["java","python","shell"]}
</pre>

2\. To enable the pretty-print, create the `Gson` object with `GsonBuilder`

    Gson gson = new GsonBuilder().setPrettyPrinting().create();
    String json = gson.toJson(obj);
    System.out.println(json);

Output

<pre>{
  "name": "mkyong",
  "age": 35,
  "position": "Founder",
  "salary": 10000,
  "skills": [
    "java",
    "python",
    "shell"
  ]
}
</pre>

3\. Full example.

GsonExample.java

    package com.mkyong.json;

    import com.google.gson.Gson;
    import com.google.gson.GsonBuilder;

    import java.math.BigDecimal;
    import java.util.ArrayList;
    import java.util.List;

    public class GsonExample {

        public static void main(String[] args) {

            Staff staff = createDummyObject();

            //Gson gson = new Gson();
            Gson gson = new GsonBuilder().setPrettyPrinting().create();

            String json = gson.toJson(staff);
            System.out.println(json);

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

<pre>{
  "name": "mkyong",
  "age": 35,
  "position": "Founder",
  "salary": 10000,
  "skills": [
    "java",
    "python",
    "shell"
  ]
}
</pre>

## Reference

1.  [GsonBuilder JavaDoc](https://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/GsonBuilder.html)

[http://www.mkyong.com/java/how-to-enable-pretty-print-json-output-gson/](http://www.mkyong.com/java/how-to-enable-pretty-print-json-output-gson/)
