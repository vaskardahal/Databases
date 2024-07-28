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
* A fact table can occupy around 90% of the entire space consumed by the DWH, every decision to store extra information in a fact table should be properly thought through and agreed upon with the business. 
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
	1. **Additive Measures**: Measures that can be summarized across <u>all</u> dimensions, including time, associated to the fact. 
	2. **Semi-additive Measures**: Measures that can be summarized across <u>some</u> dimensions, but not all. They also cannot be summarized across time. For example - an inventory table. On 1/1/2024 there were 200 items of product of X in the inventory. 100 items were sold that day, and the inventory was not replenished. So, on 1/2/2024, there are 100 items of product X in the inventory. So, what value can we really derive by adding the quantity of product X stored in the inventory on a day to day (or any temporal duration) basis? But we can definitely compare the number of items stored between different days. We can also calculate the total sum of product X and product Y stored in the inventory on a particular day. Some examples of semi-additive measures: inventory information, financial account balances, water levels on rivers, temperature  
	3. **Non-additive Measures**: Measures representing ratios or percentages or unit prices cannot be summarized across any dimension. But then, why are non-additive measures considered facts given that they provide limited possibilities for analysis? - In some cases its a matter of design preferences (storing them in fact tables vs in dimension tables as attributes). In other cases, these facts could be derived (or calculated) from other columns in the fact table - and thus remain part of the fact table. 
### Identifying the Primary Key
Fact tables express many-to-many relationship. So, a solution is required to uniquely identify the fact table rows. Various options to do so: 
1. Combine a subset a foreign keys to ensure the uniqueness of every row in the fact. This will be a multi-part key. This key is also referred to as Composite key, Compound key, Concatenated key. 
2. If a Composite key ensuring uniqueness cannot be identified, then another column from the source system can be used - for example the primary key for the transactions. This column can be merged with the subset of the FKs to create a unique rows. 
3. A Surrogate key can be maintained, just as for the dimension tables. This can be a small integer usually auto-incremented by the database, and will have no business value. In this scenario, the keys of the dimension table will not play any special role other than as simple FKs. Advantages of using a Surrogate key: 
	1. Makes it easier to identify a row in the fact table without having to navigate through multiple dimension keys. 
	2. When a data load is in progress and stops before finishing completely, sequentially incremented Surrogate key will help easily debug and find out where the load process stopped. 
	3. The update operation on a fact table can be transformed into a combination of inserts and deletes - sometimes it is more efficient to delete and insert again, instead of performing updates on large sets of data. 

### Degenerate Dimension
* Degenerate dimensions are the columns that are added to fact tables, but they are not facts and they are not keys. 
* They sometimes do look like foreign keys, but they don't point to any dimension. 
* Examples include: sales order number, invoice number, other transaction numbers. 
* Advantages of degenerate dimensions: 
	* They are usually part of the fact's PK.
	* They help grouping together all rows of the fact table that were part of the same transaction. 
	* They also help to track data back to the operational system. 
* Note that too many degenerate dimensions should not be stored, as this might massively impact the performance of the fact table. 

### Types of Fact Tables
1. **Transaction fact table**
	* The most common type of fact table found in DWH systems. 
	* Data stored in this kind of table represents a process that happened at a certain point in time - like a sales transaction that finished successfully. 
	* A row exists for a member of a dimension only if a transaction that involved that particular member happened. 
	* So, it should not be surprising if not all members from the dimension table are linked to row(s) from the the fact table. 
	* Some properties of transaction fact table are: 
		* The granularity is usually the transaction or the transaction line. 
		* They tend to become very large, storing billions or trillions of rows of data. 
		* They are usually linked to many dimensions, but they could be sparsely populated. 
		* The facts are usually additive. 
2. **Periodic Snapshot fact table**
	* Periodic snapshot fact table is populated with information as it happened at regular time interval (or at the end of the time interval) - like at the end of the day, or month. 
	* They are the second most commonly found fact tables. 
	* These tables are usually not periodically refreshed - the periodic snapshots are added on top of what already existed in the table. 
	* They are useful for analyzing trends over time. 
	* In some instances, a periodic snapshot table can be created by starting from a transaction table by adding up the transactions and showing the total of the transactions that occurred during that time period. 
3. **Accumulating Snapshot fact table**
	* These tables are used to map processes that have a clear beginning and a clear end along with a number of intermediary steps. 
	* They can used for pipeline or workflow processes  - like fulfilling an order, the progress of a mortgage application, tracking the progress of a support ticket created by a customer. 
	* Taking the example of support ticket: 
		* Each possible milestone in the process has a foreign key in the fact table. 
		* For a support ticket such milestones can be: Created ==> assigned ==> in-progress ==> in-testing ==> closed. 
		* When a process is initiated, i.e. when the ticket is created, a row in the accumulating snapshot fact table is created - with many fact columns set to their default value. 
		* As progress is made with the ticket, it is being assigned to a person and then its status is immediately changed to in-progress, the fact table row is updated with new information (like date the milestone occurred). 
	* This operation of constantly updating the fact table is not typical for the other two types of fact tables. 
	* Besides the many foreign keys for the data dimension associated with each step of the project, an accumulating snapshot table also contains more degenerate dimensions - these are columns storing the difference in time between the different milestones like the number of hours or days since the item was created until it was closed or since it was created until it was taken in-progress. 
	* These duration columns are stored more as a convenience in the fact table because even though they can be calculated on the spot by subtracting the dates from each other, they make the analysis easier when they are already present in the table. 
	* This is particularly valuable in situations where complicated calculations are required even for such seemingly simple determination of duration when we have to take into account information like national holidays, weekends, and other restrictions. 
	* Other such degenerate dimension that can occur in such accumulating transaction table are milestone completion counters - 0 for incomplete and 1 for complete. 
	* An accumulating snapshot table is usually linked to status dimension and when the row in the fact table is updated with the new milestone status, the foreign key for this dimension is also updated to reflect the current status of the project. 

### Handling Null Values
* Null values can appear and become very common in fact tables. 
* The null values can appear in these table either in the numeric measurements (i.e., in the facts) or in the FKs for the associated dimensions. 
* The first situation is more common and its alright to have null values in the facts - the aggregation functions like sum, average, min, max etc. know how to handle the nulls. 
* From the perspective of fact aggregation, replacing null with 0 would influence the aggregation calculations performed (like calculating average). 
* On the other hand, encountering a null in a fact table column declared as a foreign key to a dimension table will produce a referential integrity violation error, and this situation must be avoided. 
* The way to avoid such referential integrity violation error is with the empty row technique for the dimension tables - every dimension table should have an empty row in which all attributes are filled with values like N/A (not applicable) or Unknown. 
* When there is no link between the data in the fact row and the rows in the dimension table, the FK column from the fact is populated with the surrogate key from the empty row in the dimension. 
* This way, referential integrity is satisfied and you also have the information that for that row, a certain dimension is missing (or inapplicable). 