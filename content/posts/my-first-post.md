---
date: '2024-10-20T17:42:50+08:00'
draft: false
title: 'Apache Hadoop'
---

# Prerequisites

1. [Apache Hadoop](https://hadoop.apache.org/)
   Apache Pig is a platform build on the top of Hadoop. You can refer to our previously published article to install a Hadoop single node cluster on Windows 10.

2. [7zip](https://www.7-zip.org/)/[Winrar](https://www.win-rar.com/)
   7zip/Winrar is needed to extract .tar.gz archives we will be downloading in this guide.

# Downloading Apache Pig

Download the [Apache Pig](https://downloads.apache.org/pig/)

After the file is downloaded, we should extract it twice using **7zip** (using 7zip: the first time we extract the .tar.gz file, the second time we extract the .tar file). We will extract the Pig folder into `C:\hadoop-env` directory as used in the previous articles. Or you could use **winzip** to extract it.

# Setting Environment Variables

After extracting Derby and Hive archives, we should go to Control Panel > System and Security > System. Then Click on **Advanced system settings**.

In the advanced system settings dialog, click on **Environment variables** button.

Now we should add the following user variables:

- PIG_HOME: `C:\hadoop-env\pig-0.17.0`

![a](https://miro.medium.com/max/653/1*B3DoL0H1WYff1-fWUBK8MA.png)

> `hadoop-env` is the folder name of your hadoop.

Now, we should edit the Path user variable to add the following paths:

- %PIG_HOME%\bin

![a](https://miro.medium.com/max/527/1*ZoXoknTO6tMP9A0CNyywbA.png)

# Edit pig.cmd file

Edit file D:/Pig/pig-0.17.0/bin/pig.cmd, make below changes and save this file.

- set HADOOP_BIN_PATH=%HADOOP_HOME%\libexec

![a](https://i.ibb.co/hLpZ1w4/image.png)

# Validate Pig Installation Pig

Post successful execution of Hadoop and verify the installation.

```
C:\WINDOWS\system32>pig -version
Apache Pig version 0.17.0 (r1797386)
compiled Jun 02 2017, 15:41:58
```

> If you have encountered any problems, please read through the Troubleshooting section.

# Example Script

## Start the hadoop

Browse through the sbin directory of Hadoop and start yarn and Hadoop dfs (distributed file system) as shown below.

```
C:\WINDOWS\system32>cd %HADOOP_HOME%/sbin/
C:\WINDOWS\system32>start-all.cmd
```

> Remember to run as administrator when executing CMD.

## Create a Directory in HDFS

In Hadoop DFS, you can create directories using the command mkdir. Create a new directory in HDFS with the name Pig_Data in the required path as shown below.

```
C:\WINDOWS\system32>cd %HADOOP_HOME%/bin/
C:\WINDOWS\system32>hdfs dfs -mkdir hdfs://localhost:9000/pig_data
```

## Create a text file `wikitechy_emp_details.txt` delimited by ‘,’ with the content below. Place the file in C: or any directory which you preferred.

```
111,Anu,Shankar,23,9876543210,Chennai
112,Barvathi,Nambiayar,24,9876543211,Chennai
113,Kajal,Nayak,24,9876543212,Trivendram
114,Preethi,Antony,21,9876543213,Pune
115,Raj,Gopal,21,9876543214,Hyderabad
116,Yashika,Kannan,22,9876543215,Delhi
117,siddu,Narayanan,22,9876543216,Kolkata
118,Timple,Mohanthy,23,9876543217,Bhuwaneshwar
```

## Move the file to HDFS

Now, move the file from the local file system to HDFS using put command as shown below. (You can use copyFromLocal command as well.)

```
C:\WINDOWS\system32>cd %HADOOP_HOME%/bin/
C:\WINDOWS\system32>hdfs dfs -put C:\wikitechy_emp_details.txt hdfs://localhost:9000/pig_data/
```

## Start the Pig Grunt Shell

The simplest way to write PigLatin statements is using Grunt shell which is an interactive tool where we write a statement and get the desired output. There are two modes to involve Grunt Shell:

1. **Local**: All scripts are executed on a single machine without requiring Hadoop. (command: `pig -x local`)
2. **MapReduce**: Scripts are executed on a Hadoop cluster (command: `pig -x MapReduce`)

Since we have load the `wikitechy_emp_details.txt` in hdfs, start the Pig Grunt shell in MapReduce mode as shown below.

```
C:\WINDOWS\system32>pig -x mapreduce
```

## Load the file in a variable 'student'

Now load the data from the file student_data.txt into Pig by executing the following Pig Latin statement in the Grunt shell.

```bash
grunt> student = LOAD 'hdfs://localhost:9000/pig_data/wikitechy_emp_details.txt'
   USING PigStorage(',')
   as ( id:int, firstname:chararray, lastname:chararray, phone:chararray,
   city:chararray );
```

## Check result using DUMP operator (write result to the console)

```bash
grunt> Dump student
(111,Anu,Shankar,23,9876543210)
(112,Barvathi,Nambiayar,24,9876543211)
(113,Kajal,Nayak,24,9876543212)
(114,Preethi,Antony,21,9876543213)
(115,Raj,Gopal,21,9876543214)
(116,Yashika,Kannan,22,9876543215)
(117,siddu,Narayanan,22,9876543216)
(118,Timple,Mohanthy,23,9876543217)
```

![a](https://i.ibb.co/wrxbbDs/image.png)

> If you have encountered any problems, please read through the Troubleshooting section.

# Troubleshooting 故障排除

## Pig is not recognized as an internal or external command

```
C:\WINDOWS\system32>pig -version
'E:\hadoop-env\hadoop-3.2.1\bin\hadoop-config.cmd' is not recognized as an internal or external command,
operable program or batch file.
'-Xmx1000M' is not recognized as an internal or external command,
operable program or batch file.
```

![a](https://miro.medium.com/max/700/1*zFUaMDFADy06wQqOUGydYw.png)

Make sure your is correct

From this:

```
set HADOOP_BIN_PATH=%HADOOP_HOME%\bin
```

Change to:

```
set HADOOP_BIN_PATH=%HADOOP_HOME%\libexec
```

![a](https://i.ibb.co/hLpZ1w4/image.png)

## After `Dump` command, the process keep looping

> Pig when ran in mapreduce mode expects the JobHistoryServer to be available.

This is because the job history server is not running.

Check `marped-site.xml` has these properties stated or not.

To configure JobHistoryServer, **add** these properties to `mapred-site.xml` replacing hostname with actual name of the host where the process is started.

```xml
<property>
    <name>mapreduce.jobhistory.address</name>
    <value>hostname:10020</value>
</property>
<property>
    <name>mapreduce.jobhistory.webapp.address</name>
    <value>hostname:19888</value>
</property>
```

The result would be like this:

![a](https://i.ibb.co/ydyG8zg/image.png)

# References

1. [Solution Mandi - Cloud & Big Data !: Pig installation on Windows 10](https://www.solutionmandi.com/2018/11/pig-installation-on-windows-10.html)

2. [Apache Hadoop 2.7.1](https://hadoop.apache.org/docs/r2.7.1/hadoop-project-dist/hadoop-common/ClusterSetup.html)

3. [Not able to run dump in pig - Stackoverflow](https://stackoverflow.com/questions/42740053/not-able-to-run-dump-in-pig)

4. [pig tutorial - apache pig tutorial - Apache Pig - Running Scripts - pig latin - apache pig - pig hadoop](https://www.wikitechy.com/tutorials/apache-pig/apache-pig-running-scripts)