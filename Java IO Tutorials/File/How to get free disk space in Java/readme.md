In Java old days, it lacks of method to determine the free disk space on a partition. But this is changed since JDK 1.6 released, a few new methods – **getTotalSpace()**, **getUsableSpace()** and **getFreeSpace()**, are bundled with java.io.File to retrieve the partition or disk space detail.

## Example

    package com.mkyong;

    import java.io.File;

    public class DiskSpaceDetail
    {
        public static void main(String[] args)
        {
        	File file = new File("c:");
        	long totalSpace = file.getTotalSpace(); //total disk space in bytes.
        	long usableSpace = file.getUsableSpace(); ///unallocated / free disk space in bytes.
        	long freeSpace = file.getFreeSpace(); //unallocated / free disk space in bytes.

        	System.out.println(" === Partition Detail ===");

        	System.out.println(" === bytes ===");
        	System.out.println("Total size : " + totalSpace + " bytes");
        	System.out.println("Space free : " + usableSpace + " bytes");
        	System.out.println("Space free : " + freeSpace + " bytes");

        	System.out.println(" === mega bytes ===");
        	System.out.println("Total size : " + totalSpace /1024 /1024 + " mb");
        	System.out.println("Space free : " + usableSpace /1024 /1024 + " mb");
        	System.out.println("Space free : " + freeSpace /1024 /1024 + " mb");
        }
    }

## Output

Display the disk space detail in **c:** partition.

    === Partition Detail ===

     === bytes ===
    Total size : 52428795904 bytes
    Space free : 33677811712 bytes
    Space free : 33677811712 bytes
     === mega bytes ===
    Total size : 49999 mb
    Space free : 32117 mb
    Space free : 32117 mb

**Note**  
Both **getFreeSpace()** and **getUsableSpace()** methods are return the same total free disk space of a given partition. But the real different is not clear, even in the java doc. Tell me if you know what’s the different in between.

## Reference

[http://download.oracle.com/javase/6/docs/api/java/io/File.html](http://download.oracle.com/javase/6/docs/api/java/io/File.html)

[http://www.mkyong.com/java/how-to-get-free-disk-space-in-java/](http://www.mkyong.com/java/how-to-get-free-disk-space-in-java/)
