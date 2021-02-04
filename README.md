# 487DB-Project

A.Brief description of your data generation process 
including what program you used to generate the data?

The requirement of the project is generating a benchmark data. 
- Implement the code in Java.
- Create a new file
- Add the table and attributes like(unique1, unique2,unique3, two, four, ten, twenty, onePercent, tenPercent, 
				twentyPercent, fiftyPercent, unique3, evenOnePercent, stringu1, stringu2,string4)
- Generating the data matching with those attributes with maximum number of tuples to the table (I can adjust number of tuples)
- Write the table with generated data to new .csv file.

B.Which system you will be working with and why you chose it
  
BigQuery: 
The idea of our work is that we would run some performance experiments. So that we think about designing 
a large scale ingestion of analytics events and the system needs to be fast enough. As a result, we may 
think of Bigquery. Here is a reason why we choose Bigquery. First, Bigquery is a google analytics DB. 
Each query is transformed into an execution tree by Dremel (Google query engine).The data is retrieved 
from Colossus and aggregated…So, everything runs on Google Jupiter with a high-speed network. Second, it 
is user-friendly. It’s accessible via its web UI, command-line tool, or client library (written in C#, 
Go, Java, Node.js, PHP...Third, it has the potential to scale up. We can just stream insert data into 
the databases. Last, it has a reasonable cost. BigQuery, it’s charged per query and storage…everything 
else is free (almost). Loading data is free, but we pay for streaming insert.

PostgreSQL:
For this project we are going to run some performance experiments using postgresql. Postgresql is a popular open source SQL database. One of the reason we chose postgresql is because we have used it once before but wanted to refine our skills with using it. One of the advantages of postgresql is its a object-relational database, allowing for the support of user-defined objects. Another advantage is that it supports a extensive list of data types. A convience of using postgres is that google cloud platform makes it easy to set up a vm instance for a postgresql database. 	

C.Demonstrate you have loaded data into that system
- See the screenshots that we placed in screenshot folder.

BigQuery:

D. Include lessons learned or issues encountered
- Error loading onektup.csv file with error message "Error while reading data, error message: Error detected while
parsing row starting at position: 149. Error: Bad character(ASC II 0) Encountered". I think this error happened
when I program generating data and save to file. It was occured by writing the bad characters. To resolve this problem,
I need to clear the bad code. I loaded the file to the bucket in storage. Then run a command script on SSH in VM:

"gsutil cp gs://bucket/badfile.csv - | tr -d '\000' | gsutil cp - gs://bucket/fixedfile.csv" \

with "bucket" is yourbucket that you have created. badfile.csv and fixedfile.csv is your file that you want to fix.

- Error of accessing scope: "403 Insufficient Permission". I have spent a few minmutes to understand what problem is
And recognized because I set a default scope. It is limited to modify a file if we are not having permission. In order 
to change it, I went to Virtual Machine section and stop VM instance, Then I opened VM instance details, pressed Edit 
and change Cloud API access scope --> "Allow full access to all cloud APIs".  
  
