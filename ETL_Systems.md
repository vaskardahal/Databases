# ETL Systems
ETL is a system that incorporates all operations performed on data since it is selected from the data source until it reaches the presentation area of a Data Warehouse (DWH). It consists of 3 phases: 
1. Extraction (E)
2. Transformation (T)
3. Loading (L)
For the end users of the DWH, the ETL is like a "black box" in which the data from multiple sources is periodically gathered\integrated and transformed into meaningful reports that helps them make decisions. Therefore, the details of the ETL is not something that the end users should see or care about. But in order to provide quality and meaningful reports and complex data analysis possibilities to the users, the developers should put some serious thought into designing and implementing the ETL process.

### Types of DWH Loads
Based on the quantity of data being transferred to the DWH, there are two types of loads: 
| Full\Initial Load | Load |
|--------------|--------------|
| The process of populating the data warehouse for the first time with data from the operational system | And also |
