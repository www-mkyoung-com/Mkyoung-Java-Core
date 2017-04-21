To save byte[] into a file, try this:

    FileOutputStream fos = new FileOutputStream(fileDest);
    fos.write(bytesArray);
    fos.close();

or NIO

    Path path = Paths.get(fileDest);
    Files.write(path, bytesArray);

## Full Example

This Java Example shows you how to read a file into a byte array, and save the byte array back to a new file via the classic try-catch-try-catch, JDK 7 try-resources and Java.NIO solution.

ArrayOfBytesToFile.java

    package com.mkyong;

    import java.io.File;
    import java.io.FileInputStream;
    import java.io.FileOutputStream;
    import java.io.IOException;
    import java.nio.file.Files;
    import java.nio.file.Path;
    import java.nio.file.Paths;

    public class ArrayOfBytesToFile {

        private static final String UPLOAD_FOLDER = "C:\\temp\\";

        public static void main(String[] args) {

            FileInputStream fileInputStream = null;

            try {

                File file = new File("C:\\temp\\testing1.txt");
                byte[] bFile = new byte[(int) file.length()];

                //read file into bytes[]
                fileInputStream = new FileInputStream(file);
                fileInputStream.read(bFile);

                //save bytes[] into a file
                writeBytesToFile(bFile, UPLOAD_FOLDER + "test1.txt");
                writeBytesToFileClassic(bFile, UPLOAD_FOLDER + "test2.txt");
                writeBytesToFileNio(bFile, UPLOAD_FOLDER + "test3.txt");

                System.out.println("Done");

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
        }

        //Classic, < JDK7
        private static void writeBytesToFileClassic(byte[] bFile, String fileDest) {

            FileOutputStream fileOuputStream = null;

            try {
                fileOuputStream = new FileOutputStream(fileDest);
                fileOuputStream.write(bFile);

            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                if (fileOuputStream != null) {
                    try {
                        fileOuputStream.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            }

        }

        //Since JDK 7 - try resources
        private static void writeBytesToFile(byte[] bFile, String fileDest) {

            try (FileOutputStream fileOuputStream = new FileOutputStream(fileDest)) {
                fileOuputStream.write(bFile);
            } catch (IOException e) {
                e.printStackTrace();
            }

        }

        //Since JDK 7, NIO
        private static void writeBytesToFileNio(byte[] bFile, String fileDest) {

            try {
                Path path = Paths.get(fileDest);
                Files.write(path, bFile);
            } catch (IOException e) {
                e.printStackTrace();
            }

        }

    }

## References

1.  [How to convert File into an array of bytes](http://www.mkyong.com/java/how-to-convert-file-into-an-array-of-bytes/)
2.  [Files JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html)
3.  [FileOutputStream JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/io/FileOutputStream.html)

[http://www.mkyong.com/java/how-to-convert-array-of-bytes-into-file/](http://www.mkyong.com/java/how-to-convert-array-of-bytes-into-file/)
