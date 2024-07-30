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


<table>
<tr>
<th>Argument</th>
<th>Description</th>
</tr>
<tr>
<td>appDir</td>
<td>The top level directory that contains your app. If this option is used then
it assumed your scripts are in</td>
</tr>
<tr>
<td>baseUrl</td>
<td>By default, all modules are located relative to this path. If baseUrl is not
explicitly set, then all modules are loaded relative to the directory that holds
the build file. If appDir is set, then baseUrl should be specified as relative
to the appDir.</td>
</tr>
<tr>
<td>dir</td>
<td>The directory path to save the output. If not specified, then the path will
default to be a directory called "build" as a sibling to the build file. All
relative paths are relative to the build file.</td>
</tr>
<tr>
<td>modules</td>
<td>List the modules that will be optimized. All their immediate and deep
dependencies will be included in the module's file when the build is done. If
that module or any of its dependencies includes i18n bundles, only the root
bundles will be included unless the locale: section is set above.</td>
</tr>
</table>
