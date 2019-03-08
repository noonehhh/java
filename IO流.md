IO流

     常用：5五个类，一个接口
	     5个类：File、InputStream、OutputStream、Reader、Writer
		 1个接口：Serializable
		 
		 总结上面几种流的应用场景：

FileInputStream/FileOutputStream  需要逐个字节处理原始二进制流的时候使用，效率低下
FileReader/FileWriter 需要组个字符处理的时候使用
StringReader/StringWriter 需要处理字符串的时候，可以将字符串保存为字符数组
PrintStream/PrintWriter 用来包装FileOutputStream 对象，方便直接将String字符串写入文件 
Scanner　用来包装System.in流，很方便地将输入的String字符串转换成需要的数据类型
InputStreamReader/OutputStreamReader ,  字节和字符的转换桥梁，在网络通信或者处理键盘输入的时候用
BufferedReader/BufferedWriter ， BufferedInputStream/BufferedOutputStream ， 缓冲流用来包装字节流后者字符流，提升IO性能，BufferedReader还可以方便地

