# Run pipeline in database API
# Guideline
This document provides guideline and examples for interact with database when running pipeline. This API is an interface to help running and storage of the results of pipeline to postgre.
# Prerequisisite
# Usage
pass the pipeline jar file path, UMLS index mapping file path, thread number(optional), input source(file, folder path or JDBC configuration), output target(folder path or database table).
# Example
The following command will run the xxx pipeline on table xxx from database and store the entity table to table name xxx in database. 
java -Xmx3g -cp target/petsure-nlp-db-1.0.0.20200701-jar-with-dependencies.jar com.melax.contract.petsure.RunPipelineMain
  -c com.microsoft.sqlserver.jdbc.SQLServerDriver -i jdbc:sqlserver://petsurehistoricaldb.database.windows.net:1433;databaseName=PetsureHistoricalData   -du  melax
    -dp  Mel@xP@sswd1! -dsx NOTE_TEXT -dsi ID -dst notes_table_20190728  -p C:\Users\Administrator\Desktop\petsure-nlp-db\pipeline\petsure.pipeline.jar -I C:\Users\Administrator\Desktop\petsure-nlp-db\concept_mapping\petsure_umls_index -o jdbc:sqlserver://petsurehistoricaldb.database.windows.net:1433;databaseName=PetsureHistoricalData -dte ENT_OUT_notes_20190728 -dtr REL_OUT_notes_20190728 -t 3 -s "select ID,NOTE_TEXT from notes_table_20190728 where ID > 999991"


java -Xmx3g -cp target/petsure-nlp-db-1.0.0.20200701-jar-with-dependencies.jar com.melax.contract.petsure.RunPipelineMain
  -c com.microsoft.sqlserver.jdbc.SQLServerDriver -i jdbc:sqlserver://petsurehistoricaldb.database.windows.net:1433;databaseName=PetsureHistoricalData   -du  melax
    -dp  Mel@xP@sswd1! -dsx NOTE_TEXT -dsi ID -dst notes_table  -p C:\Users\Administrator\Desktop\petsure-nlp-db\pipeline\petsure.pipeline.jar -I C:\Users\Administrator\Desktop\petsure-nlp-db\concept_mapping\petsure_umls_index -o jdbc:sqlserver://petsurehistoricaldb.database.windows.net:1433;databaseName=PetsureHistoricalData -dte ENT_OUT_notes -dtr REL_OUT_notes -t 4 -s "select ID,NOTE_TEXT from notes_table where ID not in (select DOC_ID from ENT_OUT_notes)"


java -Xmx3g -cp target/petsure-nlp-db-1.0.0.20200701-jar-with-dependencies.jar com.melax.contract.petsure.RunPipelineMain
  -c com.microsoft.sqlserver.jdbc.SQLServerDriver -i jdbc:sqlserver://petsurehistoricaldb.database.windows.net:1433;databaseName=PetsureHistoricalData   -du  melax
    -dp  Mel@xP@sswd1! -dsx NOTE_TEXT -dsi ID -dst new_notes_table  -p C:\Users\Administrator\Desktop\petsure-nlp-db\pipeline\petsure.pipeline.jar -I C:\Users\Administrator\Desktop\petsure-nlp-db\concept_mapping\petsure_umls_index -o jdbc:sqlserver://petsurehistoricaldb.database.windows.net:1433;databaseName=PetsureHistoricalData -dte ENT_OUT_notes_new -dtr REL_OUT_notes_new -t 4 -s "select ID,NOTE_TEXT from new_notes_table where ID not in (select DOC_ID from ENT_OUT_notes_new)"






java -Xmx3g -cp target/petsure-nlp-db-1.0.0.20200701-jar-with-dependencies.jar com.melax.contract.petsure.RunPipelineMain
  -c com.microsoft.sqlserver.jdbc.SQLServerDriver -i jdbc:sqlserver://petsurehistoricaldb.database.windows.net:1433;databaseName=PetsureHistoricalData   -du  melax
    -dp  Mel@xP@sswd1! -dsx NOTE_TEXT -dsi ID -dst notes_table_20190728  -p C:\Users\Administrator\Desktop\petsure-nlp-db\pipeline\petsure.pipeline.jar -I C:\Users\Administrator\Desktop\petsure-nlp-db\concept_mapping\petsure_umls_index -o jdbc:sqlserver://petsurehistoricaldb.database.windows.net:1433;databaseName=PetsureHistoricalData -dte ENT_OUT_notes_20190728 -dtr REL_OUT_notes_20190728 -t 3 -s "select ID,NOTE_TEXT from notes_table_20190728 where ID not in (select DOC_ID from ENT_OUT_notes_20190728)"

