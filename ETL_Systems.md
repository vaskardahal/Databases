# ETL Systems
ETL is a system that incorporates all operations performed on data since it is selected from the data source until it reaches the presentation area of a Data Warehouse (DWH). It consists of 3 phases: 
1. Extraction (E)
2. Transformation (T)
3. Loading (L)
For the end users of the DWH, the ETL is like a "black box" in which the data from multiple sources is periodically gathered\integrated and transformed into meaningful reports that helps them make decisions. Therefore, the details of the ETL is not something that the end users should see or care about. But in order to provide quality and meaningful reports and complex data analysis possibilities to the users, the developers should put some serious thought into designing and implementing the ETL process.

### Types of DWH Loads
Based on the quantity of data being transferred to the DWH, there are two types of loads: 

<table>
<tr>
<th>Full/Initial Load</th>
<th>Incremental load</th>
</tr>
<tr>
<td>Process of populating the DWH for the first time with data from the operational system</td>
<td>Process of updating the DWH by only bringing in the changes to the operation system</td>
</tr>
<tr>
<td>All fact and dimension table are truncated and reloaded</td>
<td> Fact and dimension table are never truncated, just updated with new info</td>
</tr>
<tr>
<td>Old data is lost</td>
<td>Existing/Old data is preserved</td>
</tr>
<tr>
<td>Takes a lot of time to execute and complete</td>
<td>Loading incrementally takes less time than a full load</td>
</tr>
<tr>
<td>Easy to implement since no history is preserved in the DWH</td>
<td>
	Technical implementation, however, is more complex because: 
	<ul>
		<li> Need to keep track of previous load date </li>
		<li> Find a way to store multiple versions of the same source row in the dimension table to keep track of updates </li>
	</ul>
</td>
</tr>
</table>

#### Incremental Load Elements
* Add an auxiliary table (also known as "Incremental loads" table) that will keep track of the dates when each table was loaded. 
* Add **Valid from** and **Valid to** columns in all dimension tables to keep track of versions.

### Data Lineage
* Data Lineage tracks the movement of data. Information kept track of by Data Lineage: 
	* What are the origins of the data
	* Where is the data going to in the DWH (which fact or dimension table)
	* When was the data last loaded or updated
	* What transformations are applied to the data
* The complexity of the implementation of Data Lineage tracking can vary according to the necessity of the DWH project
* Advantages of having Data Lineage tracking are: 
	* Troubleshooting and Debugging becomes easier
	* Increases trustworthiness of the data
	* Makes the business rules applied to data more obvious and transparent
	* Helps to validate the integrity of the DWH during data audits
* What to do to implement Data Lineage: 
	* Ensure uniqueness of each row in the DWH:
		* Use surrogate key in each table. In a larger DWH, data passes multiple stages from source to destination. Passing this unique ID through all these stages will help to trace back the data
	* Keep track of the operation that loaded each row:
		* For this, a new column called "Lineage" could be added to each table, and populate it with the key of the ETL operation that loaded the data

## ETL Tools
A system comprised of all the components needed to build ETL process. 

It has various components: 
* Data flow management
* Connectors to other systems
* Data transformation components
* Logging and auditing
* Debugging
* Deployment

Advantages of using an ETL Tool: 
* Flexibility - Has more capabilities than writing code and SQL queries as it has almost everything built in. Data can be easily be transformed, strings can be manipulated in creative ways, lookups can be performed, data can be matched and profiled.  
* Maintainability - It's a lot easier to maintain and extend a solution created in ETL system, as opposed to working with 100s of stored procedures and custom functions. Also, ETL tools are very graphical and easy to interpret. 
* Performance - ETL tools allow tasks to run in parallel, perform in-memory lookups or transformations, distribute the tasks on multiple servers for faster execution
* Logging and audit - Provide built-in capabilities for logging, auditing and documenting the data operations
* 