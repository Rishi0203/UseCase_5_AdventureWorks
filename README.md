<h1>Case Study Adventure Works</h1>
<h3>Aim</h3>
<p>To perform Hive analytics on Sales and Customer Demographics data using big data tools such as Sqoop, Spark, and HDFS..</p>

<h3>Problem Statement</h3>
<p>
We will dig deeper into some of the Hive's analytical features for this hive project. Using SQL is still highly popular, and it will be for the foreseeable future. Most big data technologies have been modified to allow users to interact with them using SQL. This is due to the years of experience and expertise put into training, acceptance, tooling, standard development, and re-engineering. So, in many circumstances, employing these excellent SQL tools to access data may answer many analytical queries without resorting to machine learning, business intelligence, or data mining.
This big data project will look at Hive's capabilities to run analytical queries on massive datasets. We will use the Adventure works dataset in a MySQL dataset for this project, and we'll need to ingest and modify the data. We'll use Adventure works sales and Customer demographics data to perform analysis and answer the following questions:</p>

<ul>
 <li>Which age group of customers contribute to more sales?</li>
 <li>To find the upper and lower discount limits offered for any product</li> 
 <li>Sales contributions by customer</li>
 <li>To Understand customer persona purchasing pattern based on gender, education and yearly income</li>
 <li>To find the sales contribution by customers on the overall year to date sales belong to categorized by same gender, yearly income.</li>
 <li>To identify the top performing territory based on sales</li>
 <li>To find the territory-wise sales and their adherence to the defined sales quota.</li>
</ul>

<h3>Technologies used to work in project</h3>
<h5>MySQL</h6>
<h5>HDFS Ecosystem</h5>

<ul>
 <li>Sqoop</li>
 <li>Hive</li>
 <li>PySpark</li>
</li>
</ul>  

<h3>Data Source Description</h3>
<p>Adventure Works is a free sample database of retail sales data. In this project, we will be only using Customer test, Individual test, Credit card, Sales order details, Store, Sales territory, Salesperson, Sales order header, Special offer tables from this database.</p>
<p>&nbsp;&nbsp; &nbsp;&nbsp;  <b>Customer Individual</b>: This table contain all customer data related information.</p>
<p>&nbsp;&nbsp; &nbsp;&nbsp;  <b>Individual</b>: This table contain all Individual data information.</p>
<p>&nbsp;&nbsp; &nbsp;&nbsp;  <b>Credit Card</b>: This table contain all credit card data information.</p>


![image](https://user-images.githubusercontent.com/100192276/159165809-b0e591e2-9b0e-404e-9f04-41a25f6b8ac9.png)


<h3>Project Architecture</h3>

![Advan](https://user-images.githubusercontent.com/100192276/159118171-900a13d7-f750-410c-bd78-be85008e8c92.jpg)

<h3>Steps performed to achive the task</h3>
<ul>
 <li>Create tables in MySQL database.</li>
 <li>Load data from MySQL into HDFS storage using Sqoop commands.</li>
 <li>Move data from HDFS to Hive.</li>
 <li>Integrate Hive into Spark and perform data cleaning.</li>
 <li>Using Pyspark, extract Customer demographics information from data and store it as parquet files.</li>
 <li>Move parquet files from Spark to Hive.</li>
 <li>Create tables in Hive and load data from Parquet files into tables.</li>
 <li>Perform Hive analytics on Sales and Customer demographics data.</li>
</ul>






