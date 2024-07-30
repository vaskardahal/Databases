# SQL Functions


### ISNULL()
* Used to handle NULL value
* Can only take 2 parameters:
	* First parameter represents the expression we want to check if it evaluates to NULL or not. 
	* Second parameter represents the expression we want to replace the first parameter is, if the first parameter evaluates to NULL. 
### COALESCE()
* Used to handle NULL value
	```
	SELECT COALESE(FirstName, '') + 
		COALESE(MiddleName, '') + 
		COALESE(LastName, '') 
	FROM Person;
	```
* Evaluates arguments and always returns the first non-NULL value
	```
	SELECT FirstName, LastName, 
		COALESCE(HomePhone, WorkPhone, CellPhone, 'NA') PhoneNumber
	FROM EmergencyContact;
	```
* Replaces NULL values with user-defined value
* For multiple arguments, the data types of expressions must be same
* COALESE() is just a syntactic shortcut for the CASE expression in SQL

## SQL Window Functions
