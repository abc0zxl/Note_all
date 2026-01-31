# Apache POI

他是用来处理Office的各种文件格式的开源项目

**作用**：再java程序中对office文件进行读写操作。

**一般情况下都是excel的操作**


**实际应用场景**：

1.银行网银系统导出交易明细

2.各种业务系统导出excel报表

3.批量导入数据



### 创建Excel文件，并写入

1.创建一个方法叫write

2.再内存中创建对象XSSFWorkbook excel = new XSSFWorkbook（）；

3.**excel中创建sheet页**：

* XSSFSheet sheet=excel.createSheet("info");

4.**sheet中创建行对象**：

* XSSFRow row=sheet.createRow(1);

5.**在行上创建单元格对象**：

* XSSFCell cell=row.createCell(1);

6.**向单元格对象里写入内容**：

* cell.setCellValue("姓名"）；
* cell.setCellValue("城市"）；

![image.png](/assets/6c67b702-b1ef-4de8-a3c2-c2cb5bda9ebf.png)

* 如果想在别的行写入数据，就需要创建对应行数的行对象

7.**通过输出流将文件写入到磁盘**

* FileOutputStream out=new FileOutputStream(new file("D:\\info.xlse"))
* excel.write(out);

8.**关闭资源**

* out.close();
* excel.close();


### Excel读取

1.**创建一个方法**：名字叫做read

2.**读取操作，创建一个输入流对象，导入excel文件**：

FileInputStream file=new FileInputStream(("D:\\info.xlsx"));

3.**创建excel对象,将输入流读取的导入**：

XSSFWorkbook excel=new XSSFWorkbook(file);

4.**读取excel中第一个sheet页**：

XSSFSheet sheet1=excel.getSheetAt(0);

5.**获取Sheet页中最后一行的行号**：

int lastRowNum=sheet.getLastRowNum();

6.**遍历每一行的数据**：用for循环

![image.png](/assets/aeda77ad-1290-4f67-a428-e7ecbef3dcd4.png)



### 导出包含信息的Excel报表步骤

1.**设计Excel模板文件**：会有一个excel模板，有标题等公共信息。然后通过程序在对应位置填入数据即可。

![image.png](/assets/1e95c5a9-b29d-4a99-8fbe-6ca917509139.png)


2.**查询近30天运营数据**

* 调用别的service方法查询某一区域的数据集群，得到数据
* 获取到模板excel文件到**输入流对象中**
* ![image.png](/assets/3751cf78-6ac5-4f99-be33-64b05cbe022d.png)
* 上面图片中差个后缀.xlsx

3.**将查询到的数据写入模板**

* 基于上面的in来创建一个excel文件对象
* 将查到的数据写入excel模板中，插入方法如上面的方法
* ![image.png](/assets/e1a6dbcb-68ca-4ba6-95ad-72a97c5084dd.png)

4.**通过输出流将Excel文件下载到客户端浏览器**

* 这里要将这个文件下载到客户端浏览器需要用到**response输出流**
* 新建一个输出流对象，将excel文件放进去
* 通过response对象返回这个excel输出流对象

5.**关闭资源**

![image.png](/assets/046955ae-ad0a-4a8f-9bbb-d38e59bbdd59.png)




#### 写入多行数据

1.查询数据

2.获取目标行对象

3.一个一个导入改行数据

4.循环到第一步

![image.png](/assets/03dd830d-b36a-4268-aa5a-1945a683f027.png)
