---
title: "Development guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/hdfs_development_guide"
---

<span id="_1-hdfs-的初始化"></span>
## **1 HDFS initialization**

Before performing development operations using the HDFS API, HDFS must be initialized. There are generally two ways to initialize HDFS:


1. Directly load the configuration files from the HDFS cluster, such as the core\-site.xml and hdfs\-site.xml files.

2. Manually load HDFS cluster information using methods provided by the conf object, such as cluster name, replication factor, and so on.


Here, only the first method is introduced:

```java
Configuration conf = new Configuration();//Initialize the conf variable
private void init() throws IOException {
        conf = new Configuration();
        //Assume that the following two configuration files have both been copied to the conf directory
        conf.addResource("conf/hdfs-site.xml");
        conf.addResource("conf/core-site.xml");
        fSystem = FileSystem.get(conf);
}

```


After initializing the HDFS file system, you can use the APIs provided by HDFS for development.

The main dependencies used are hadoop\-common, hadoop\-hdfs, and hadoop\-client.

<span id="_2-上传和下载文件"></span>
## **2 Uploading and downloading files**

```java
private static void uploadTest() throws Exception{
    //Here, local_src.txt is a local file, and hdfs_dst.txt is the file uploaded to hdfs
    fSystem.copyFromLocalFile(new Path("local_src.txt"), new Path("hdfs_dst.txt"));
    fSystem.close();
}

```


```java
private static void downloadTest() throws Exception{
    //Here, hdfs_src.txt is a file on hdfs, and local_dst.txt is the file downloaded from hdfs
    fSystem.copyToLocalFile(new Path("hdfs_src.txt"), new Path("local_dst.txt"));
    fSystem.close();
}

```


The underlying implementation of the upload and download APIs is actually FileUtil.copy(....).

**Of course, you can also upload and download files using streams.** 

```java
private static void uploadTest() throws Exception{
    //local.gz is a file on the local file system, and hdfs.gz is a file on hdfs
    InputStream in = new FileInputStream(new File("local.gz"));
    FSDataOutputStream out = fSystem.create(new Path("/hdfs.gz"));
    IOUtils.copyBytes(in, out, 4096, true);
    fSystem.close();
}

```


```java
private static void downloadTest() throws Exception{
    //Here, hdfs.gz is a file on hdfs, and local.gz is the file downloaded to the local file system
    FSDataInputStream in = fs.open(new Path("/hdfs.gz"));
    OutputStream out = new FileOutputStream(new File("local.gz"));
    IOUtils.copyBytes(in, out, 4096, true);
    fSystem.close();
}

```


<span id="_3-写文件和追加写文件"></span>
## **3 Writing files and appending to files**

```java
private void createFileAndWrite() throws IOException {
    //Write the contents of content to the hdfs file Write.txt
    final String content = "So well!";
    FSDataOutputStream out = null;
    try {
        out = fSystem.create(new Path("/user/Write.txt"));
        out.write(content.getBytes());
        out.hsync();
    } finally {
            // make sure the stream is closed finally.
            out.close();
 }
}

```


```java
private void appendFileContents() throws IOException {
    //Append the contents of content to the hdfs file Write.txt
    final String content = "hi boy";
    FSDataOutputStream out = null;
    try {
        out = fSystem.append(new Path("/user/Write.txt"));
        out.write(content.getBytes());
        out.hsync();
} finally {
        // make sure the stream is closed finally.
        out.close();
 }
}

```


If the file to be appended, Write.txt, already exists and no other client is writing to it at the same time. Otherwise, the append operation will fail and throw an exception.

<span id="_4-读文件"></span>
## **4 Reading files**

Obtain an input stream for reading a file by calling the open method of the FileSystem instance. Then use this input stream to read the contents of the specified file on HDFS. Finally, call close() to close the input stream.

```java
private void read() throws IOException {
//Read the contents of a file
    String strPath = "/user/Reader.txt";
    Path path = new Path(strPath);
    FSDataInputStream in = null;
    BufferedReader reader = null;
    StringBuffer strBuffer = new StringBuffer();
    try {
        in = fSystem.open(path);
        reader = new BufferedReader(new InputStreamReader(in));
        String sTempOneLine;
        // write file
        while ((sTempOneLine = reader.readLine()) != null) {
             strBuffer.append(sTempOneLine);
        }
    LOG.info("the content is : " + strBuffer.toString());

    } finally {
    IOUtils.closeStream(reader);
    IOUtils.closeStream(in);
     }
}

```


<span id="_5-删除文件"></span>
## **5 Deleting files**

```java
private void deleteFile() throws IOException {

    //Delete the following files and make them unrecoverable
    Path beDeleted = new Path("/user/fileDelete.txt");
    boolean res=fSystem.delete(beDeleted, true);
    System.out.println(res);
}

```


<span id="_6-嵌套创建目录与递归删除目录"></span>
## **6 Creating nested directories and recursively deleting directories**

```java
private static void testMkDir() throws Exception{

    //Create nested directories
    boolean mkdirs = fSystem.mkdirs(new Path("/user/test1/test2"));
    System.out.println("mkdirs success!");
}

```


```java
private static void testDel() throws Exception{

    //Recursively delete directories
    if (!fSystem.exists("/user/test1")) {//Directory does not exist
            return false;
    }
    boolean delBl = fSystem.delete(new Path("/user/test1"), true);
    System.out.println(delBl);
}
```


<span id="_7-递归查看目录下文件以及块的信息"></span>
## **7 Recursively viewing files and block information in a directory**

```java
private static void listFilesAndBlocks()throws Exception{

    //List all files in the specified directory; here, the root directory under hdfs is used as an example
    RemoteIterator<LocatedFileStatus> listFiles = fSystem.listFiles(new Path("/"), true);
    while(listFiles.hasNext()){
        LocatedFileStatus file = listFiles.next();
        System.out.println(file.getPath()+"\t");
        System.out.println(file.getPath().getName()+"\t");
        System.out.println(file.getLen()+"\t");
        System.out.println(file.getReplication()+"\t");

        //Obtain information related to blocks
        BlockLocation[] blockLocations = file.getBlockLocations();
        System.out.println(blockLocations.length+"\t");
        for(BlockLocation bl : blockLocations){
            String[] hosts = bl.getHosts();
            System.out.print(hosts[0] + "-" + hosts[1]+"\t");
         }
   }
}

```


To avoid recursive viewing, set the parameter in fSystem.listFiles to false.

For more detailed information about the HDFS API, refer to the Apache Hadoop community documentation.
