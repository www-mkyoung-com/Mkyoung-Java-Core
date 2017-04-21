To convert a file to byte[], try this :

    File file = new File("/temp/abc.txt");
    //init array with file length
    byte[] bytesArray = new byte[(int) file.length()];

    FileInputStream fis = new FileInputStream(file);
    fis.read(bytesArray); //read file into bytes[]
    fis.close();

    return bytesArray;

or NIO

    String filePath = "/temp/abc.txt";

    byte[] bFile = Files.readAllBytes(new File(filePath).toPath());
    //or this
    byte[] bFile = Files.readAllBytes(Paths.get(filePath));

## Full Example

This Java Example show you how to read a file into a byte array, using the classic `FileInputStream` and also the `java.nio`classes.

FileToArrayOfBytes.java

    package com.mkyong;

    import java.io.File;
    import java.io.FileInputStream;
    import java.io.IOException;
    import java.nio.file.Files;
    import java.nio.file.Path;
    import java.nio.file.Paths;

    public class FileToArrayOfBytes {

        public static void main(String[] args) {

            try {

                // convert file to byte[]
                byte[] bFile = readBytesFromFile("C:\\temp\\testing1.txt");

                //java nio
                //byte[] bFile = Files.readAllBytes(new File("C:\\temp\\testing1.txt").toPath());
                //byte[] bFile = Files.readAllBytes(Paths.get("C:\\temp\\testing1.txt"));

                // save byte[] into a file
                Path path = Paths.get("C:\temp\\test2.txt");
                Files.write(path, bFile);

                System.out.println("Done");

                //Print bytes[]
                for (int i = 0; i < bFile.length; i++) {
                    System.out.print((char) bFile[i]);
                }

            } catch (IOException e) {
                e.printStackTrace();
            }

        }

        private static byte[] readBytesFromFile(String filePath) {

            FileInputStream fileInputStream = null;
            byte[] bytesArray = null;

            try {

                File file = new File(filePath);
                bytesArray = new byte[(int) file.length()];

                //read file into bytes[]
                fileInputStream = new FileInputStream(file);
                fileInputStream.read(bytesArray);

            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                if (fileInputStream != null) {
                    try {
                        fileInputStream.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }

            }

            return bytesArray;

        }

    }

## References

1.  [Java – How to save byte[] to file](http://www.mkyong.com/java/how-to-convert-array-of-bytes-into-file/)
2.  [Files JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html)
3.  [FileInputStream JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/io/FileInputStream.html)

[http://www.mkyong.com/java/how-to-convert-file-into-an-array-of-bytes/](http://www.mkyong.com/java/how-to-convert-file-into-an-array-of-bytes/)
