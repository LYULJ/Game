# Run pipeline in database API
# ![alt text](https://user-images.githubusercontent.com/31905713/62812961-de2c0680-bacd-11e9-943a-0e5c45ddf33b.png "Logo Title Text 1")

 
## Guideline
This document provides guideline and examples for interact with database when running pipeline. This API is an interface to help running and storage of the results of pipeline to postgre.
## Prerequisisite
Postgre

## Usage
pass the pipeline jar file path, UMLS index mapping file path, thread number(optional), input source in the form of text file, folder path or JDBC configuration and database table, output target in the form of folder path or database table as argumengs upon run the program.

## Examples
The following command will run the petsure.pipeline pipeline on NOTE_TEXT,ID,notes_table_20190728 table in PetsureHistoricalData database and store the entity table named ENT_OUT_notes_20190728 and the relation table named REL_OUT_notes_20190728 in PetsureHistoricalData table in database. The query statement inplement on this table is "select ID,NOTE_TEXT from notes_table_20190728 where ID > 999991". The specified UMLS index file is petsure_umls_index.
```
$java -Xmx3g -cp target/petsure-nlp-db-1.0.0.20200701-jar-with-dependencies.jar com.melax.contract.petsure.RunPipelineMain -c com.microsoft.sqlserver.jdbc.SQLServerDriver -i jdbc:sqlserver://petsurehistoricaldb.database.windows.net:1433;databaseName=PetsureHistoricalData   -du  melax -dp Mel@xP@sswd1! -dsx NOTE_TEXT -dsi ID -dst notes_table_20190728  -p C:\Users\Administrator\Desktop\petsure-nlp-db\pipeline\petsure.pipeline.jar -I C:\Users\Administrator\Desktop\petsure-nlp-db\concept_mapping\petsure_umls_index -o jdbc:sqlserver://petsurehistoricaldb.database.windows.net:1433;databaseName=PetsureHistoricalData -dte ENT_OUT_notes_20190728 -dtr REL_OUT_notes_20190728 -t 3 -s "select ID,NOTE_TEXT from notes_table_20190728 where ID > 999991"

```

The following command will run the petsure.pipeline pipeline on data in notes_table_20190728.txt in input folder and store the output to folder output
```
$java -Xmx3g -cp target/petsure-nlp-db-1.0.0.20200701-jar-with-dependencies.jar com.melax.contract.petsure.RunPipelineMain
  -c com.microsoft.sqlserver.jdbc.SQLServerDriver -i C:\Users\Administrator\Desktop\input\notes_table_20190728.txt  -p C:\Users\Administrator\Desktop\petsure-nlp-db\pipeline\petsure.pipeline.jar -I C:\Users\Administrator\Desktop\petsure-nlp-db\concept_mapping\petsure_umls_index -o C:\Users\Administrator\Desktop\output
```    
  ## Command Line Options
### General
| Option        | Description           | 
| ------------- |:-------------:|
| -p            | Path of the pipeline jar file | 
| -l            | License path and filename      |  
| -i            | Directory path of the input file or folder  |   
| -o            | Directory path of the output file folder|
| -U            | UMLS username|
| -P            |UMLS password|
| -I            |Directory path of the umls index folder|

### for JDBC configuration 
| Option        | Description           | 
| ------------- |:-------------:|
| -c            | JDBC Driver class name | 
| -du            | Database username      |  
| -dp            | Database password  |   
| -dst           | Source database tablename|
| -dsi            | Source database table, ID fieldname|
| -dsx            |Source database table, TEXT fieldname|
| -dsd            |Source database table, text date fieldname|
| -dtt            |Target tablename|
|-dte             |Target tablename for named entity|
|-dtr             |Target tablename for relation      |
|-s               |SQL statement to retrieve text file|

### Optional
|Option|Description|
| ------------- |:-------------:|
|-t|Number of threads to run|
|-h| Print help for this application|
  

