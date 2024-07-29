# SQL Functions


### COALESCE()
* Used to handle NULL value
```
	SELECT COALESE(FirstName, '') + 
		COALESE(MiddleName, '') + 
		COALESE(LastName, '') 
	FROM Person;
```
* Evaluates arguments and always returns the first non-null value
	```
	SELECT FirstName, LastName, 
		COALESCE(HomePhone, WorkPhone, CellPhone, 'NA') PhoneNumber
	FROM EmergencyContact;
	```
* Replaces null values with user-defined value
* 

## SQL Window Functions
