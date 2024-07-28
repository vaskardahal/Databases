[<--](DataWarehousing.md)

# Fact Table
* In a company, several business process take place everyday. Sales transaction, salary increase, signing a contract - all these are day to day business processes. 
* These business processes can be measured - quantities of products sold, price of products sold, number of contract, number of customers acquired etc. 
* A fact table keeps track of the different outputs of a **single** business process. 
* It is used in combination with the data from dimension tables for: 
	* Reporting purposes - How many units of product X were sold last week? 
	* Measuring performance - Is the summer promotion reaching its targets? 
	* Analyzing trends over time - Was the customer acquisition/churn more or less than last year? 
* Fact table contains a lot of measurements and thus tends to grow very fast. So, performance should always be an important design factor. 
* Despite having numerous rows, DWH users do not analyze the Fact table rows one by one. That information is already available in the operational systems. Rather, they carry out aggregation analysis over thousands or millions of rows of facts. 
* Because of the need for such aggregation, it is vital that fact table measurements have same level of detail or granularity. For example, a single fact table should not contain sales amount per product and also sales amount for the entire transaction (which could be composed of multiple products). 
* If different granularities are used per fact table row, the aggregation will generate incorrect results. 
## Structure of a Fact table
The main elements of a Fact table are: 
1. Facts - Columns storing the measurements of the process
2. Primary key - Uniquely identifies rows
3. Foreign keys - Linking the fact table with the dimension tables

## Steps for Identifying Facts
1. Analyze what is important about a certain business process. 
2. During such analysis, multiple possible facts (or measures) will be identified. 
3. While analyzing in which fact table to store them, its important to remember that all measurements should have the same level of detail or granularity. 
4. Its also important to remember that not all numeric data coming out of a process is a valued fact. One basic rule that can be applied for identifying facts is to test if they can be summed up by one or more dimensions, or if they can be aggregated over time. Example - Sales amount can be summed up by product, date, customer, or any other involved dimension. On the other hand, customers' social security number or invoice number do not make much sense to aggregate, and therefore, they do not qualify as valid facts. 
5. So the main property of a measurement that will qualify it as a valid fact is **additivity**. There are various kinds of measures based on their additivity level: 
	1. Additive Measures: Measures that can be summarized across <u>all</u> dimensions, including time, associated to the fact. 
	2. Semi-additive Measures: Measures that can be summarized across <u>some</u> dimensions, but not all. They also cannot be summarized across time. For example - an inventory table. On 1/1/2024 there were 200 items of product of X in the inventory. 100 items were sold that day, and the inventory was not replenished. So, on 1/2/2024, there are 100 items of product X in the inventory. So, what value can we really derive by adding the quantity of product X stored in the inventory on a day to day (or any temporal duration) basis? But we can definitely compare the number of items stored between different days. We can also calculate the total sum of product X and product Y stored in the inventory on a particular day. Some examples of semi-additive measures: inventory information, financial account balances, water levels on rivers, temperature  
	3. Non-additive Measures: Measures representing ratios or percentages or unit prices cannot be summarized across any dimension. But then, why are non-additive measures considered facts given that they provide limited possibilities for analysis? - In some cases its a matter of design preferences (storing them in fact tables vs in dimension tables as attributes). In other cases, these facts could be derived (or calculated) from other columns in the fact table - and thus remain part of the fact table. 
### Identifying the Primary Key
Fact tables express many-to-many relationship. So, a solution is required to uniquely identify the fact table rows. Various options to do so: 
1. Combine a subset a foreign keys to ensure the uniqueness of every row in the fact. This will be a multi-part key. This key is also referred to as Composite key, Compound key, Concatenated key. 
2. If a Composite key ensuring uniqueness cannot be identified, then another column from the source system can be used - for example the primary key for the transactions. This column can be merged with the subset of the FKs to create a unique rows. 
3. A Surrogate key can be maintained, just as for the dimension tables. This can be a small integer usually auto-incremented by the database, and will have no business value. In this scenario, the keys of the dimension table will not play any special role other than as simple FKs. Advantages of using a Surrogate key: 
	1. Makes it easier to identify a row in the fact table without having to navigate through multiple dimension keys. 
	2. When a data load is in progress and stops before finishing completely, sequentially incremented Surrogate key will help easily debug and find out where the load process stopped. 
	3. The update operation on a fact table can be transformed into a combination of inserts and deletes - sometimes it is more efficient to delete and insert again, instead of performing updates on large sets of data. 
4. 