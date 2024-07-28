# Databases vs Data Warehouses vs Data Lakes

## Databases
1. Focuses on operational/transactional data.
2. Queried/Interacted with on a day to day basis. 
3. Highly normalized data model. 
4. Built to manage CRUD operations quickly and efficiently. 
5. Usually row-based data modeling. 
6. Queries are generally simple and very fast. 
7. Don't always track historical information. 

## Data Warehouses
A Data Warehouse as a subject-oriented, integrated, time-variant, non-volatile collection of data in support of management's decision-making process. 
1. Centralizes and integrates business operational data. 
2. Used by analysts, data scientists and other business users to build dashboard, reporting and other analytical purposes. 
3. Most data models are de-normalized. 
4. Built to manage analytics & aggregations quickly. 
5. Columnar data model for efficiency. 
6. Queries are often complex & often take long to execute. 
7. Tracks historical information. 
8. Very rigid schema. So, changing schema is very slow. 

## Data Lakes
1. Schema-on-read - i.e., schema is not defined while writing data to the Data Lake. 
2. Can store structured, semi-structured, non-structured data - kinda like a folder system. 
3. Used by data scientists/ data engineers unless another layer like Hive is put on top of it. 
4. Built to process large amounts of data at a lower cost than data warehouse. 
5. Tracks historical information, but it is not as well-structured as Data Warehouse is. 
6. Very flexible and easy to make changes to. 
7. Has HDFS Architecture (???). 
   