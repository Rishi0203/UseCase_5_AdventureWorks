<h3>Create MySQL View</h3>
<p><b>CREATE VIEW</b> customer_individual as select a.CustomerID, a.TerritoryID, a.AccountNumber, a.CustomerType, a.ModifiedDate, b.Demographics <br>
<b>FROM</b> customer a, individual b <br>
<b>WHERE</b> a.CustomerID = b.CustomerID;</p>


<h3>Importing Customer & Individual Data From Mysql To HDFS Using Sqoop</h3>
<p><b>SQOOP IMPORT</b> \<br>
&nbsp;&nbsp;&nbsp;&nbsp;--<b>CONNECT</b> jdbc:mysql://localhost:3306/adventureworks?useSSL=False \<br>
&nbsp;&nbsp;&nbsp;&nbsp;--<b>USERNAME</b>  ${USERNAME} --PASSWORD-FILE ${PASSWORD} \<br>
&nbsp;&nbsp;&nbsp;&nbsp;--<b>DELETE-TARGET-DIR</b> --TARGET-DIR ${DIR} \<br>
&nbsp;&nbsp;&nbsp;&nbsp;--<b>QUERY</b> "select CustomerID,TerritoryID,AccountNumber,CustomerType,ModifiedDate,Demographics FROM customer_individual \<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>WHERE</b> \$CONDITIONS" --SPLIT-BY CustomerID</p>

<h3>Importing Credit Card data From MySQL to HDFS using Sqoop</h3>
<p><b>SQOOP IMPORT</b> \<br>
&nbsp;&nbsp;&nbsp;&nbsp;--<b>CONNECT</b> jdbc:mysql://localhost:3306/adventureworks?useSSL=False \<br/>
&nbsp;&nbsp;&nbsp;&nbsp;--<b>USERNAME</b> ${USERNAME} --PASSWORD-FILE ${PASSWORD} \<br>
&nbsp;&nbsp;&nbsp;&nbsp;--<b>DELETE-TARGET-DIR</b> --TARGET-DIR ${DIR1} \<br>
&nbsp;&nbsp;&nbsp;&nbsp;--<b>QUERY</b> "SELECT CreditCardID,CardType,CardNumber,ExpMonth,ExpYear,ModifiedDate FRM creditcard \<br>
&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp; <b>WHERE</b> \$CONDITIONS" -m 1

<h3>Creating Hive managed table for customer date & loading the data</h3>
<p><b>CREATE TABLE</b> cust_indi(CustomerID int, TerritoryID int, AccountNumber string, CustomerType string, ModifiedDate timestamp, <br/>&nbsp;&nbsp;&nbsp;&nbsp; Demographics string) <br> 
   &nbsp;&nbsp;&nbsp;&nbsp;<b>ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' <br>
   &nbsp;&nbsp;&nbsp;&nbsp;TBLPROPERTIES("skip.header.line.count"="1");</b><br>
   &nbsp;&nbsp;&nbsp;&nbsp;<b>LOAD DATA INPATH</b> "/user/saif/HFS/Input/adventureworks/" <b>INTO TABLE</b> cust_indi;</p>

<h3>Organizing the XML data into separate columns and loading the data in the new customer table</h3>
<p>
<b> CREATE TABLE</b> ext_cust <b>AS SELECT </b> customerid, territoryid, accountnumber, customertype, modifieddate, &nbsp;&nbsp;&nbsp;&nbsp;<b>XPATH</b>(demographics,'IndividualSurvey/TotalPurchaseYTD/text()'), <b>XPATH</b>(demographics,'IndividualSurvey/DateFirstPurchase/text()'), &nbsp;&nbsp;&nbsp;&nbsp;<b>XPATH</b>(demographics,'IndividualSurvey/BirthDate/text()'), <b>XPATH</b>(demographics,'IndividualSurvey/MaritalStatus/text()'), &nbsp;&nbsp;&nbsp;&nbsp;<b>XPATH</b>(demographics,'IndividualSurvey/YearlyIncome/text()'), <b>XPATH</b>(demographics,'IndividualSurvey/Gender/text()'), &nbsp;&nbsp;&nbsp;&nbsp;<b>XPATH</b>(demographics,'IndividualSurvey/TotalChildren/text()'), <b>XPATH</b>(demographics,'IndividualSurvey/NumberChildrenAtHome/text()'), &nbsp;&nbsp;&nbsp;&nbsp;<b>XPATH</b>(demographics,'IndividualSurvey/Education/text()'), <b>XPATH</b>(demographics,'IndividualSurvey/Occupation/text()'), &nbsp;&nbsp;&nbsp;&nbsp;<b>XPATH</b>(demographics,'IndividualSurvey/HomeOwnerFlag/text()'), <b>XPATH</b>(demographics,'IndividualSurvey/NumberCarsOwned/text()'), &nbsp;&nbsp;&nbsp;&nbsp;<b>XPATH</b>(demographics,'IndividualSurvey/CommuteDistance/text()')
<br><b>FROM</b> cust_indi;</p>

</p>
<h3>Creating managed table for credit card & Loading the data</h3>
<p><b>CREATE TABLE</b> credit_hive(CreditCardID int,CardType string,CardNumber bigint,ExpMonth int,ExpYear int,ModifiedDate timestamp ) <br>
 &nbsp;&nbsp;&nbsp;&nbsp;<b>ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' <br>
 &nbsp;&nbsp;&nbsp;&nbsp;TBLPROPERTIES("skip.header.line.count"="1");</b><br>
 &nbsp;&nbsp;&nbsp;&nbsp;<b>LOAD DATA INPATH</b> "/user/saif/HFS/Input/adventureworks1/" <b>INTO TABLE</b> credit_hive;</p>

