# Assignment A-2 MapReduce Commands:
```bash
start-all.sh
jps
sudo mkdir analyser_log
ls
sudo chmod -R 777 ~/analyser_log
sudo chown -R hadoop ~/analyser_log/
```
## Move all java files from downloads folder to home/analyser_log folder
```bash

cd analyser_log/
ls
sudo chmod +r "."
ls
```
## For Hadoop Version 2.10.2 
```bash
export CLASSPATH="$HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-client-core-2.10.2.jar:$HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-client-common-2.10.2.jar:$HADOOP_HOME/share/hadoop/common/hadoop-common-2.10.2.jar:~/analyser_log/SalesCountry/*:$HADOOP_HOME/lib/*"
```

## For Hadoop Version 3.2.1
```bash

export CLASSPATH="$HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-client-core-3.2.1.jar:$HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-client-common-3.2.1.jar:$HADOOP_HOME/share/hadoop/common/hadoop-common-3.2.1.jar:~/analyser_log/SalesCountry/*:$HADOOP_HOME/lib/*"
```

```bash
javac -d . SalesCountryDriver.java SalesCountryReducer.java SalesMapper.java
ls
cd SalesCountry/
ls
cd ..
sudo gedit manifest.txt
```
## Add the following lines into manifest.txt file.
```
Main-Class: SalesCountry.SalesCountryDriver
```
```bash
jar -cfm analyser_log.jar manifest.txt SalesCountry/*.class
ls
```
```bash
sudo mkdir ~/input400
$HADOOP_HOME/bin/hadoop fs -mkdir /input400
$HADOOP_HOME/bin/hdfs dfs -put /home/hadoop/Downloads/SalesJan2009.csv /input400/
$HADOOP_HOME/bin/hadoop jar analyser_log.jar /input400 /output400
```
