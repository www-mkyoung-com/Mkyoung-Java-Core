To create a directory in Java, uses the following code:

1\. Standard Java IO package – `java.io.File`

1.1 Create a single directory.

    new File("C:\\Directory1").mkdir();

1.2 Create a directory named “Directory2 and all its sub-directories “Sub2” and “Sub-Sub2” together.

    new File("C:\\Directory2\\Sub2\\Sub-Sub2").mkdirs()

_P.S Both method `mkdir()` and `mkdirs()` are returning a boolean value to indicate the operation status : true if succeed, false otherwise._

2\. For JDK 7, try Java NIO package – `java.nio.file.Paths` and `java.nio.file.Files`

    Path path = Paths.get("C:\\Directory1");
    Files.createDirectories(path);

## 1\. Java IO Example

A classic Java IO directory example, check if directory exists, if no, then create it.

CreateDirectoryExample.java

    package com.mkyong.file;

    import java.io.File;

    public class CreateDirectoryExample {

        public static void main(String[] args) {

            File file = new File("C:\\Directory1");
            if (!file.exists()) {
                if (file.mkdir()) {
                    System.out.println("Directory is created!");
                } else {
                    System.out.println("Failed to create directory!");
                }
            }

            File files = new File("C:\\Directory2\\Sub2\\Sub-Sub2");
            if (!files.exists()) {
                if (files.mkdirs()) {
                    System.out.println("Multiple directories are created!");
                } else {
                    System.out.println("Failed to create multiple directories!");
                }
            }

        }

    }

## 2\. Java NIO Example

Java NIO classes are added in JDK 7.

CreateDirectoryExample.java

    package com.mkyong.file;

    import java.io.IOException;
    import java.nio.file.Files;
    import java.nio.file.Path;
    import java.nio.file.Paths;

    public class CreateDirectoryExample {
        public static void main(String[] args) {

            Path path = Paths.get("C:\\Directory2\\Sub2\\Sub-Sub2");
            //if directory exists?
            if (!Files.exists(path)) {
                try {
                    Files.createDirectories(path);
                } catch (IOException e) {
                    //fail to create directory
                    e.printStackTrace();
                }
            }

        }

    }

If a directory is failing to create, `IOException` will be thrown, for example

<pre>java.nio.file.AccessDeniedException: /directory-name
	at sun.nio.fs.UnixException.translateToIOException(UnixException.java:84)
	at sun.nio.fs.UnixException.rethrowAsIOException(UnixException.java:102)
	at sun.nio.fs.UnixException.rethrowAsIOException(UnixException.java:107)
	at sun.nio.fs.UnixFileSystemProvider.createDirectory(UnixFileSystemProvider.java:384)
	at java.nio.file.Files.createDirectory(Files.java:674)
	at java.nio.file.Files.createAndCheckIsDirectory(Files.java:781)
	at java.nio.file.Files.createDirectories(Files.java:767)
</pre>

## References

1.  [java.nio.file.Files JavaDoc](https://docs.oracle.com/javase/7/docs/api/java/nio/file/Files.html)
2.  [java.io.File JavaDoc](https://docs.oracle.com/javase/7/docs/api/java/io/File.html)
3.  [Java NIO tutorials](http://tutorials.jenkov.com/java-nio/index.html)

[http://www.mkyong.com/java/how-to-create-directory-in-java/](http://www.mkyong.com/java/how-to-create-directory-in-java/)
