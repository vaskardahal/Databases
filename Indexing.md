# Database Indexing

## How data is stored in Table? 
Let's look a the following table: 
| Emp ID  | Name  | Address  | 
|---------|--------|----------|
|      1       |       A    |    City A  | 
|      2       |       B    |    City B  | 
|      3       |       C    |    City C  | 
|      4       |       D    |    City D  | 

This is just a logical representation of the data. The actual data is not stored in this way. 

On the backend, the DBMS will create **Data Pages** (which is generally 8KB depending upon DB). And each Data Page can store multiple rows in it. 

Schematic representation of a typical Data Page: 


```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```
