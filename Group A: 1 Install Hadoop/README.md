# Installing Hadoop on Ubuntu

Follow the steps below to install Hadoop on Ubuntu:

1. Update the system packages:
```
sudo apt-get update
```

2. Install OpenJDK 8:
```
sudo apt install openjdk-8-jdk
```

3. Navigate to the JVM directory:
```
cd /usr/lib/jvm
```

4. List the files in the directory:
```
cd /usr/lib/jvm
```

5. Go back to the home directory:
```
cd
```

6. Open the `.bashrc` file for editing:
```
sudo nano .bashrc
```

7. Add the following lines at the end of the file:
```bash
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export PATH=$PATH:/usr/lib/jvm/java-8-openjdk-amd64/bin
export HADOOP_HOME=~/hadoop-3.3.4/
export PATH=$PATH:$HADOOP_HOME/bin
export PATH=$PATH:$HADOOP_HOME/sbin
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
export HADOOP_STREAMING=$HADOOP_HOME/share/hadoop/tools/lib/hadoop-streaming-3.3.4.jar
export HADOOP_LOG_DIR=$HADOOP_HOME/logs
export PDSH_RCMD_TYPE=ssh
```
8. Save the changes by pressing Ctrl+O, then press Enter. Exit the editor by pressing Ctrl+X.

9. Install SSH:

sudo apt-get install ssh

10. Download & Extract the Hadoop archive:
Download from here : https://dlcdn.apache.org/hadoop/common/hadoop-3.3.4/hadoop-3.3.4.tar.gz
```javascript
tar -zxvf ~/Downloads/hadoop-3.3.4.tar.gz
```
11. Navigate to the Hadoop configuration directory:

```bash
cd hadoop-3.3.4/etc/hadoop
```

12. List the files in the directory:

```bash
ls
```
13. Open the hadoop-env.sh file for editing:
```
sudo nano hadoop-env.sh
```
14. Uncomment the line that sets JAVA_HOME and set the path for JAVA_HOME:

```javascript
JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
```

15. Save the changes by pressing Ctrl+O, then press Enter. Exit the editor by pressing Ctrl+X.

16. Open the core-site.xml file for editing:
```
sudo nano core-site.xml
```
17. Add the following configuration at the end of the file:
```
<configuration>
  <property>
    <name>fs.defaultFS</name>
    <value>hdfs://localhost:9000</value>
  </property>
  <property>
    <name>hadoop.proxyuser.dataflair.groups</name>
    <value>*</value>
  </property>
  <property>
    <name>hadoop.proxyuser.dataflair.hosts</name>
    <value>*</value>
  </property>
  <property>
    <name>hadoop.proxyuser.server.hosts</name>
    <value>*</value>
  </property>
  <property>
    <name>hadoop.proxyuser.server.groups</name>
    <value>*</value>
  </property>
</configuration>
```
18. Save the changes by pressing Ctrl+O, then press Enter. Exit the editor bypressing Ctrl+X.

19. Open the hdfs-site.xml file for editing:
```
sudo nano hdfs-site.xml
```
Add the following configuration at the end of the file:
```<configuration>
  <property>
    <name>dfs.replication</name>
    <value>1</value>
  </property>
</configuration>
```
21. Save the changes by pressing Ctrl+O, then press Enter. Exit the editor by pressing Ctrl+X.

22. Open the mapred-site.xml file for editing:
```
sudo nano mapred-site.xml
```

23. Add the following configuration at the end of the file:
```
<configuration>
  <property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
  </property>
  <property>
    <name>mapreduce.application.classpath</name>
    <value>$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*:$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*</value>
  </property>
</configuration>
```
24. Save the changes by pressing Ctrl+O, then press Enter. Exit the editor by pressing Ctrl+X.

25. Open the yarn-site.xml file for editing:
sudo nano yarn-site.xml

26. Add the following configuration at the end of the file:
```<configuration>
  <property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
  </property>
  <property>
    <name>yarn.nodemanager.env-whitelist</name>
    <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>
  </property>
</configuration>
```
27. Save the changes by pressing Ctrl+O, then press Enter. Exit the editor by pressing Ctrl+X.

28. Configure SSH for localhost:
```
ssh localhost
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
```

29. Format the Hadoop filesystem:
```
hadoop-3.3.4/bin/hdfs namenode -format
```

30. Set the PDSH_RCMD_TYPE environment variable:
```
export PDSH_RCMD_TYPE=ssh
```

31. Start Hadoop:
```
start-all.sh
```

32. Open the following URL in your browser to access the Hadoop web interface:
```
localhost:9870
```
