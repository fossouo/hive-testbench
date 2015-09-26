A. Check your installation of javac on your OS $

[root@master hive-testbench]# alternatives --install /usr/bin/javac javac /usr/jdk64/jdk1.8.0_40/bin/javac 20000
[root@master hive-testbench]# alternatives --set javac /usr/jdk64/jdk1.8.0_40/bin/javac

B. Build the test : tpcds-build.sh 

./tpcds-build.sh

C. generate data :
 
 ./tpcds-setup.sh 1000  (generate 1 TB of data)

The advantage of this version of hivebench is that it comes with all file integrate (not the official one : ex tpcds_kit.zip)

D. Some examples:

Build 1 TB of TPC-DS data: ./tpcds-setup 1000

Build 1 TB of TPC-H data: ./tpch-setup 1000

Build 100 TB of TPC-DS data: ./tpcds-setup 100000

Build 30 TB of text formatted TPC-DS data: FORMAT=textfile ./tpcds-setup 30000

Build 30 TB of RCFile formatted TPC-DS data: FORMAT=rcfile ./tpcds-setup 30000

E. Run queries.

More than 50 sample TPC-DS queries and all TPC-H queries are included for you to try. You can use hive, beeline or the SQL tool of your choice. The testbench also includes a set of suggested settings.

This example assumes you have generated 1 TB of TPC-DS data during Step 5:

cd sample-queries-tpcds
hive -i testbench.settings
hive> use tpcds_bin_partitioned_orc_1000;
hive> source query55.sql;

Note that the database is named based on the Data Scale chosen in previous step. At Data Scale 10000, your database will be named tpcds_bin_partitioned_orc_10000. At Data Scale 1000 it would be named tpcds_bin_partitioned_orc_1000. You can always show databases to get a list of available databases.

Similarly, if you generated 1 TB of TPC-H data during the previous Step :

 cd sample-queries-tpch
 hive -i testbench.settings
 hive> use tpch_bin_partitioned_orc_1000;
 hive> source tpch_query1.sql;
