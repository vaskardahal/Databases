
# Table of Contents
* Data Warehousing
* [ETL Systems](ETL_Systems.md)

# Data Warehousing
## Background
### Problems that Data Warehouse can solve
1. When there is a lot of data, and we can't make much out of such overwhelming volume of data => Data Warehouse helps bring in only the data that is important and relevant for the purpose. 
2. When the data must be sliced and diced and analyzed by all possible angle. 
3. When the business people, who usually are not experts in data and its usage, need to access the data easily. 
4. Standardizing the KPI numbers between different departments so that there is a consistent baseline. 
5. Allows to make decisions based on facts without having to rely upon assumptions. 

### Requirements of a Data Warehouse Solution
1. Easily accessible - it should be easily understood by business users, also the BI tools used for analyzing the data from all angles should also be simple to use.
2. Fast - query results should be returned to the users with minimal wait times but within realistic expectations. 
3. Consistent - The data in the Warehouse should be consistent and trustworthy.
4. Flexible - Company strategies are changing fast and with them the user needs, business conditions, data and technology may also change. The solution should be easy to change, modify and enhance if required, without invalidating existing data and reporting systems. 
5. Secure - The system should be secure enough for storing confidential information, and access to the system should be able to be controlled at a granular level. 
6. Foundation of decision-making - This is the core value of a BI system. Right data should be shown to the users at right time so that they can make informed decision. 

### Responsibilities of a Data Warehouse Designer
1. Understand the business users 
2. Deliver high-quality, relevant, and accessible information
3. Sustain the DW environment

## Dimensional Modeling
Dimensional Modeling is a database design method optimized for data warehouse solutions. This is a popular technique because it address two important requirements: 
1. Deliver data in an understandable format. 
2. Deliver fast query performance. 
### Elements of a Dimensional Modeling
1. Facts
2. Dimensions
3. Attributes of Dimensions
4. Star schema (and/or OLAP cubes)
#### Fact Table and Facts
1. The rows in a fact table will always have 1:1 relationship between fact table row and real-world event (like transactions)
2. Most facts should be additive (though some are not)
3. Fact table will have foreign keys (FK) to dimension tables
4. Fact table always has a primary key (PK) which is usually a composite key composed of a subset of foreign keys
#### Dimension Table and Dimensions
1. Dimension Tables are companions to a fact table.
2. Dimension table describe all the context associated with a business process measurement event - they answer questions like who, what, where, when, how, why associated with the event.
3. There is no limit on how many attributes a dimension can have.
4. Dimension tables usually have less rows than fact tables - but they can become much wider.
5. A dimension table is defined by a **single** primary key (PK) which is going to be referred in the fact table - PK is the basis for the referential integrity with the fact table. 
6. Dimension tables are de-normalized tables - which is also another reason for having so many attributes. Flattened many-to-one relationships within a single dimension table. 
#### Attributes
1. The attributes of a dimension tables are the primary source of query constraints, groups and report labels. 
2. The quality of attributes $\propto$ quality of the system. 
3. Attributes should consist of real words rather than cryptic abbreviations and they should consist of descriptive words or expressions instead of codes. 
4. Also null values in the source should be replaced with meaningful words - like unknown, not applicable, does not exist. 
5. Flags and indicators ((1 or 0 and True or False)) should be replaced with their more comprehensive textual counterparts - for example, the attribute "IsWeekend" in data source with a value of 0 & 1 can be represented in DW as an attribute "Weekend_Indicator" with a value of "Weekday" or "Weekend". 
#### Star Schema
1. Simple and symmetric.
2. Each dimension is an entry point to a fact table. 
3. Symmetrical structure allows effective handling of complex queries. 
4. Its highly recognizable by the business users. 
5. Easily extensible to accommodate change 
	1. A new dimension table can be added and link this dimension to the related facts table, by making sure that a row in the dimension table can be linked to a row in the facts table. 
	2. We can add a completely new fact table and link it to the existing dimensions. 

[Dimension Table](DimensionTable)

[Fact Table](FactTable.md)

### Four-step Dimensional Design Process
1. Select the business process to be modeled. Business process is a low-level activity performed by an organization to accomplish a certain goal - like taking phone orders, receiving payments, handling support calls, paying the vendors. 
2. Declare the granularity of the the model - identify the level of detail of a business process we want to measure. 
3. Identify the dimensions and dimension attributes. 
4. Identify the facts - by answering the question what is the process measuring. All candidate facts must be true to the grain for that fact table. And facts with different grains should be split in separate tables. 

Note that these steps do not need to be performed in the exact order. Sometimes we first ask what business problem are we trying to solve or what facts are we trying to find, and go on from there. 

### Relationship between fact and dimension
There is a **many-to-many** relationship between the the fact and dimension. Examples:
1. In one sale, there can be multiple products. And one product can be part of many sales. 
2. Multiple promotions can be applied to a single sale. And obviously, the same promotion can be applied to multiple sales. 



## Data to work on
1. Walmart Case Study
2. 





