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
		<li> Find a way to store multiple versions of the same source row in the dimension table to keep track of updates <li>
	</ul>
</td>
</tr>
</table>

