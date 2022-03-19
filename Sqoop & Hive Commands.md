<h3>Importing Customer & Individual Data From Mysql To HDFS Using Sqoop</h3>
<p>sqoop import --connect jdbc:mysql://localhost:3306/adventureworks?useSSL=False --username root
--password-file file:///home/saif/LFS/cohort_c9/envvar/sqoop.pwd --delete-target-dir --target-dir /user/saif/HFS/Input/adventureworks
--query "select CustomerID,TerritoryID,AccountNumber,CustomerType,ModifiedDate,Demographics from customer_individual
where $CONDITIONS" --split-by CustomerID</p>

<h3>Creating Hive managed table for customer date & loading the data</h3>
<p>create table cust_indi(CustomerID int,TerritoryID int,AccountNumber string,CustomerType string,ModifiedDate timestamp,Demographics string) \ row format delimited fields terminated by ',' tblproperties("skip.header.line.count"="1") ;
load data inpath "/user/saif/HFS/Input/adventureworks/" into table cust_indi;</p>

<h3>Organizing the XML data into separate columns and loading the data in the new customer table</h3>
<p>create table ext_cust as select customerid,territoryid,accountnumber,customertype,modifieddate,xpath(demographics,'IndividualSurvey/TotalPurchaseYTD/text()'),xpath(demographics,'IndividualSurvey/DateFirstPurchase/text()'),xpath(demographics,'IndividualSurvey/BirthDate/text()'),xpath(demographics,'IndividualSurvey/MaritalStatus/text()'),xpath(demographics,'IndividualSurvey/YearlyIncome/text()'),xpath(demographics,'IndividualSurvey/Gender/text()'),xpath(demographics,'IndividualSurvey/TotalChildren/text()'),xpath(demographics,'IndividualSurvey/NumberChildrenAtHome/text()'),xpath(demographics,'IndividualSurvey/Education/text()'),xpath(demographics,'IndividualSurvey/Occupation/text()'),xpath(demographics,'IndividualSurvey/HomeOwnerFlag/text()'),xpath(demographics,'IndividualSurvey/NumberCarsOwned/text()'),xpath(demographics,'IndividualSurvey/CommuteDistance/text()') from cust_indi;</p>
<h3>Importing Credit Card data From MySQL to HDFS using Sqoop</h3>
<p>sqoop import --connect jdbc:mysql://localhost:3306/adventureworks?useSSL=False --username root --password-file file:///home/saif/LFS/cohort_c9/envvar/sqoop.pwd --delete-target-dir --target-dir /user/saif/HFS/Input/adventureworks1 --query "select CreditCardID,CardType,CardNumber,ExpMonth,ExpYear,ModifiedDate from creditcard \ where \$CONDITIONS" -m 1
Creating managed table for credit card & Loading the data
create table credit_hive(CreditCardID int,CardType string,CardNumber bigint,ExpMonth int,ExpYear int,ModifiedDate timestamp ) row format delimited fields terminated by ',' tblproperties("skip.header.line.count"="1");
load data inpath "/user/saif/HFS/Input/adventureworks/" into table credit_hive;</p>

<h3>Loading the data from Hive to Pyspark For Transformation</h3>
<h3>Loading the data from Pyspark to Hive and perform analytics</h3>
