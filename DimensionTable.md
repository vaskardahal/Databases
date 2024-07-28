## Dimension Table Design Techniques
#### How is Dimension Table different from a Relation Table? 
- Normalization rules do not apply in dimension table. 
- It is not optimized for data modification aspect (INSERT, UPDATE, DELETE).
- Integrates multiple data sources in a consistent way. 
- Data is easy to read by the user. 
#### Surrogate Key
* The most common relationship between a dimension and fact table is is one-to-many - a row in the dimension to many rows in fact table. Example, a chocolate chip cookie (a product) was sold to 3 customers (multiple transactions). Thus a table relationship is created with the help of keys - primary key of the dimension table and foreign key of the fact table. 
* Therefore, it is important to consider how the primary key of the dimension table is created, since it plays an important role in the BI solution: 
	* Some developers use the PK from the source systems. But it is not a good practice. This is because when the dimension table is derived from multiple source systems, and there is an overlap in values of the primary keys for two different items. 
	* A good practice is to generate a separate unique key for this dimension table, and also include the source (or original key) in a different column. 
* A common practice is to generate an artificial key - for example a simple integer column that gets incremented automatically every time a new row is added to the table. This way, this key doesn't need to be maintained, and there will be no overlapping values either. 
* In DW terminology, this is called a **Surrogate Key**. The Surrogate key has been called other names as well - Meaningless key, Integer key, Non-natural key, Artificial key, synthetic key. 
* There are multiple advantages of using a Surrogate key: 
	* Surrogate key allows to integrate multiple source systems into one single table. 
	* Surrogate key allows to keep track of changes to data (attributes) over time. A common technique for handling changes to dimension attributes is the use of surrogate keys to handle multiple versions for a single row in the source system - one way to identify different versions are by incorporation of time attributes like valid-from and valid-to. 
	* Surrogate key protects the data warehouse from operational changes by acting as a buffer - When the historical row from the operational systems from which the dimension table is sourced deleted, the dimension table doesn't need to delete it too. The only change needed is updating the valid-to and valid-from column to the relevant row in the dimension table. 
	* Surrogate key participates in the handling of null or unknown conditions - empty row technique (*dive deeper*)
	* Surrogate key helps improve performance - Surrogate key is usually an integer. And the fact table usually includes surrogate keys of many dimension tables as FKs. The number of rows in a fact table can grow very quickly, so the size of the integer of the FK integer can make a huge difference as every byte counts. 
#### Business Key
* The primary key of the original data source systems stored as a dimension attribute is called Business key. This is called a business key because it comes from the business system. It also has alternative names like Natural key, Production key, Operational key. 
* Business keys are modeled as attributes of dimension table and will not be used as keys, despite their name. 
* If there are multiple source systems, the business keys can be prefixed (or suffixed) with an identifier of the source so that a user can easily determine what source a particular record came from. 
* If the same item is represented in more than one data source, and its required to know where the data came from, business key can provide that information. 
* If the BK is composed of meaningful code, the code should be split and each code stored in separate column (dimension attribute). 
### Hierarchies in Dimension Table
