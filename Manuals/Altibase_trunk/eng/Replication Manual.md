Replication Manual
================

#### Trunk

Altibase® Administration

<br><br><br><br><br><br>
<!-- PDF 변환을 위한 여백입니다. --> 







































<!-- PDF 변환을 위한 여백입니다. --> 

<div align="left">
    <img src="media/common/e5cfb3761673686d093a3b00c062fe7a.png">
</div>

<br><br><!-- PDF 변환을 위한 여백입니다. --> 





























<!-- PDF 변환을 위한 여백입니다. --> 

<pre>
Altibase Administration Replication Manual
Trunk
Copyright ⓒ 2001~2023 Altibase Corp. All Rights Reserved.<br>
This manual contains proprietary information of Altibase® Corporation; it is provided under a license agreement containing restrictions on use and disclosure and is also protected by copyright patent and other intellectual property law. Reverse engineering of the
software is prohibited.<br>
All trademarks, registered or otherwise, are the property of their respective owners.<br>
<b>Altibase Corp</b>
10F, Daerung PostTower II,
306, Digital-ro, Guro-gu, Seoul 08378, Korea
Telephone : +82-2-2082-1000 
Fax       : +82-2-2082-1099
Customer Service Portal : <a href='http://support.altibase.com/en/'>http://support.altibase.com/en/</a>
Homepage                : <a href='http://www.altibase.com'>http://www.altibase.com</a></pre>

<br>

# Table Of Contents

- [Preface](#preface)
  - [About This Manual](#about-this-manual)
- [1. Replication Overview](#1-replication-overview)
  - [Introduction](#introduction)
- [2. Managing Replication](#2-managing-replication)
  - [Replication Procedures](#replication-procedures)
  - [Troubleshooting](#troubleshooting)
  - [Conflict Resolution](#conflict-resolution)
  - [Eager Replication Failback](#eager-replication-failback)
  - [Parallel Replication](#parallel-replication)
  - [Performance View related to Replication](#performance-view-related-to-replication)
- [3. Deploying Replication](#3-deploying-replication)
  - [Considerations](#considerations)
  - [CREATE REPLICATION](#create-replication)
  - [Starting, Stopping and Modifying Replication using “ALTER REPLICATION”](#starting-stopping-and-modifying-replication-using-alter-replication)
  - [DROP REPLICATION](#drop-replication)
  - [Extra Features](#extra-features-1)
  - [Replication in a Multiple IP Network Environment](#replication-in-a-multiple-ip-network-environment)
  - [Replication Related Properties](#replication-related-properties)
- [4. Executing DDL Statements in a Replication Environment](#4-executing-ddl-statements-in-a-replication-environment)
  - [Overview](#overview)
  - [Allowed DDL Statements](#allowed-ddl-statements)
  - [Executing DDL Statements](#executing-ddl-statements)
  - [DDL Execution Example](#ddl-execution-example)
- [5. Executing DDL Synchronization](#5-executing-ddl-synchronization)
  - [Overview](#overview-1)
  - [How to Perform DDL Synchronization](#how-to-perform-ddl-synchronization)
  - [DDL Synchronization Example](#ddl-synchronization-example)
- [6. Fail-Over](#6-fail-over)
  - [Fail-Over Overview](#fail-over-overview)
  - [Callback - JDBC](#callback---jdbc)
  - [Using Fail-Over](#using-fail-over)
  - [Writing Callback in JDBC](#writing-callback-in-jdbc)
  - [SQLCLI](#sqlcli)
  - [Embedded SQL](#embedded-sql)
  - [PDO - Callback](#pdo---callback)
- [7. Sequence Replication](#7-sequence-replication)
  - [Sequence Replication](#sequence-replication)
- [8. ROLE](#8-role)
  - [Log Analyzer Role](#log-analyzer-role)
  - [Propagation](#propagation)
- [Appendix A: FAQ](#appendix-a-faq)
  - [Replication FAQ](#replication-faq)
- [Appendix B: Standard DDL Execution Procedure](#appendix-b-standard-ddl-execution-procedure)
  - [Environment Where Service Stop is Possible](#environment-where-service-stop-is-possible)
  - [Environment Where Service Cannot Be Stopped](#environment-where-service-cannot-be-stopped)
- [Appendix C: SQL Apply Mode](#appendix-c-sql-apply-mode)
  - [Overview](#overview-3)
  - [Conditions for SQL Apply Mode Operation](#conditions-for-sql-apply-mode-operation)
  - [Setting the SQL Apply Mode](#setting-the-sql-apply-mode)


# Preface
### About This Manual

This manual explains the concepts, components, and basic use of Altibase.

#### Audience

This manual has been prepared for the following Altibase users:

-   Database managers
-   Performance managers
-   Database users
-   Application developers
-   Technical support engineers

It is recommended for those reading this manual possess the following background knowledge:

-   Basic knowledge in the use of computers, operating systems, and operating system utilities
-   Experience in using relational databases and understanding of database concepts
-   Computer programming experience
-   Experience in database server management, operating system management, or network administration

#### Organization

This manual has been organized as follows:

-   Chapter 1: Introduction  
    This chapter provides an overview of Altibase replication

-   Chapter 2: Managing Replication  
    This chapter explains how to manage Altibase replication.

-   Chapter 3: Deploying Replication  
    This chapter explains how to deploy Altibase replication.

-   Chapter 4: Executing DDL Statements in a Replication Environment
    
    This chapter explains how to execute DDL statements in a replication environment.
    
-   Chapter 5: DDL Synchronization
    
    This chapter describes the DDL Synchronization feature.
    
-   Chapter 6: Fail-Over  
    This chapter explains the Fail-Over feature provided by Altibase and how to use it.

-   Chapter 7: Sequence Replication   
    This chapter describes how to use the sequence replication that Altibase provides.
    
-   Chapter 8: ROLE   
    This chapter explains how to configure the system to perform special functions by assigning ROLE to replication.
    
-   Appendix A. FAQ   
    This chapter provides FAQs related to Altibase replication and replication properties.
    
-   Appendix B. Executing DDL Statements for Replication Targets

    This appendix explains how to execute DDL statements on replication targets without changing property settings.

-   Appendix C. SQL Apply Mode

    This appendix describes the SQL Apply mode used in various replication operations.

#### Documentation Conventions

This section describes the conventions used in this manual. Understanding these conventions will make it easier to find information in this manual and other manuals in the series.

There are two sets of conventions:

-   Syntax diagrams
-   Sample code conventions

##### Syntax diagrams

This manual describes command syntax using diagrams composed of the following elements:

| Elements                                         | Meaning                                                      |
| ------------------------------------------------ | ------------------------------------------------------------ |
| ![](media/Replication/Replication_eng.1.2.1.jpg) | Indicates the start of a command. If a syntactic element starts with an arrow, it is not a complete command. |
| ![](media/Replication/image006.gif)              | Indicates that the command continues to the next line. if a syntactic element ends with this symbol, it is not a complete command. |
| ![](media/Replication/image008.gif)              | Indicates that the command continues from the previous line. If a syntactic element starts with this symbol, it is not a complete command. |
| ![](media/Replication/image010.gif)              | Indicates the end of a statement.                            |
| ![](media/Replication/image012.gif)              | Indicates a mandatory element.                               |
| ![](media/Replication/image014.gif)              | Indicates an optional element.                               |
| ![](media/Replication/image016.gif)              | Indicates a mandatory element comprised of options. One, and only one, option must be specified. |
| ![](media/Replication/image018.gif)              | Indicates an optional element comprised of options           |
| ![](media/Replication/image020.gif)              | Indicates an optional element in which multiple elements may be specified. A comma must precede all but the first element. |

##### Sample Code Conventions

The code examples explain SQL, stored procedures, iSQL, and other command line syntax.

The following describes the conventions used in the code examples:

| Rules            | Meaning                                                      | Example                                                      |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [ ]              | Indicates an optional item                                   | VARCHAR [(*size*)] [[FIXED \|] VARIABLE]                     |
| { }              | Indicates a mandatory field for which one or more items must be selected. | { ENABLE \| DISABLE \| COMPILE }                             |
| \|               | A delimiter between optional or mandatory arguments.         | { ENABLE \| DISABLE \| COMPILE } [ ENABLE \| DISABLE \| COMPILE ] |
| . . .            | Indicates that the previous argument is repeated, or that sample code has been omitted. | SQL\> SELECT ename FROM employee;<br/> ENAME<br/>  -----------------------<br/> SWNO<br/>  HJNO<br/>  HSCHOI<br/>  .<br/> .<br/> .<br/> 20 rows selected. |
| Other Symbols    | Symbols other than those shown above are part of the actual code. | EXEC :p1 := 1; acc NUMBER(11,2)                              |
| Italics          | Statement elements in italics indicate variables and special values specified by the user. | SELECT \* FROM *table_name*; <br/>CONNECT *userID*/*password*; |
| Lower case words | Indicate program elements set by the user, such as table names, column names, file names, etc. | SELECT ename FROM employee;                                  |
| Upper case words | Keywords and all elements provided by the system appear in upper case. | DESC SYSTEM_.SYS_INDICES_;                                   |

#### Related Documents

Please refer to the following documents for more detailed information:

-   Installation Guide

-   Administrator’s Manual

-   Getting Started Guide

-   SQL Reference

-   iSQL User’s Manual

-   Error Message Reference

#### Altibase Welcomes Your Comments and Feedback

Please let us know what you like or dislike about our manuals. To help us with better future versions of our manuals, please tell us if there are any corrections or classifications that you would find useful.

Include the following information: 

-   The name and version of the manual that you are using
-   Any comments about the manual
-   Your name, address, and phone number

If you need immediate assistance regarding any errors, omissions, and other technical issues, please contact [Altibase's Support Portal](http://support.altibase.com/en/).

Thank you. We always welcome your feedback and suggestions.

# 1. Replication Overview

### Introduction

The purpose of database replication is to maintain an up-to-date backup of the data on an Active Server and provide an uninterrupted service environment in which a substitute server can be used to resume service in the event that the Active Server unexpectedly goes offline for some reason.

This chapter covers the following subjects::

-   Altibase Replication Concepts and Terminology
-   Replication Function in Altibase
-   Choosing Replication Targets
-   Replication mode
-   Replication and Data Definition Language (DDL)
-   Data Recovery Using Replication

#### Concepts

The log replay method is the basis of the Altibase replication functionality. First, a local server transfers transaction logs to a remote server when the logs change. Then the remote server “replays” the received logs to its database (that is, it implements the changes that have been recorded in the logs). Altibase also provides the altiComp utility for monitoring and managing the replication status. 

For more detailed information, please refer to the *Utilities Manual*.

#### Terminology

-   **Local Server:**  
    In this manual, the term "local server" always refers to the local node (that is, to the server on which the current task is performed), regardless of whehter it is an Active or Standyby Server, or whether it hosts a replication Sender or Receiver thread.
    
-   **Remote Server:**  
    This is a counterpart replication node (i.e., a node that has a 1:1 relationship with a local server to form a replication pair).
    
-   **Active Server:**  
    Among the database servers that are connected in replication, this is a replication node that is actively providing service to users and on which change operations related to master transacitons take place. 
    
-   **Standby Server:**  
    This is a replication node on which change transactions are not occurring. (It may be queried using SELECT statements).
    
-   **Sender:**  
    This is a thread that sends information about changes made to data caused by a transaction to a remote server. It changes logs that result from the execution of DML statements on replication target tables on the local server into XLog form so that they contain information about the actual (physical) changes made to the data and sends the resultant XLogs to the remote server.
    
-   **Receiver:**  
    This is a thread that receives XLogs (which contain information about changes to data) from a counterpart server. If there is no applier, the receiver replays the Logs on replication target objects on the local node. 
    
-   **Applier:**  
    This term indicates a thread that applies the XLog that the sender sent to the receiver, to the Storage Manager. 
    
    If the parallel receiver applier option is omitted, the receiver takes the role of the applier, and the applier is not created. 
    
-   **Ahead Analyzer:**  
    If the replication transaction grouping option has been specified and a replication gap occurs, this thread analyzes logs (before the sender does) and creates replication transaction groups. Replication transaction groups help dissolve gaps; the sender references these transaction groups to adjust the amount of XLogs it sends to the receiver.
    
-   **Sender Thread:**  
    This has the same meaning as "Sender" when not using parallel replication (i.e., when performing replication using only one Sender thread and one Receiver thread). When using parallel replication, one Sender consists of multiple Sender threads.
    
-   **Receiver Thread:**  
    This has the same meaning as "Receiver" when not using parallel replication (i.e., when performing replication using only one Sender thread and one Receiver thread). When using parallel replication, one Receiver consists of multiple Receiver threads.
    
-   **XSN:**  
    This stands for "XLog Sequence Number". It is not to be confused with "SN" (the sequence number of a redo log).

-   **Local Commit XSN:**  
    This is the sequence number of the committed log record that was most recently read by the Sender. The transaction corresponding to this XSN is not guaranteed to have been committed on the remote server. This value is returned when the COMMIT_XSN column of the V$REPSENDER performance view is queries. 
    
-   **Restart Sequence Number SN:**  
    This is the lowest Redo SN (not XSN) corresponding to a transaction for which an XLog for replication has not been sent. It is the position from which the transmission of XLogs will recommence when replication resumes.
    
-   **XLog:**  
    This is a kind of log that results from the transformation of one or more redo logs into logical form for replication. The replication Sender thread on a local server transmits an XLog to the replication Receiver thread on a remote server, which then replays the log so that the remote server contains the same data as the local server
    
-   **Master Transaction:**  
    This is a transaction taht takes place on an Active server when providing service to users. It involves the execution of one of more change (INSERT, UPDATE, or DELETE) operations on on or more replication targe tables.
    
-   **Replication Transaction:**  
    This is a transaction that replicates a master transaction on another server. It replays the execution of one or more change (INSERT, UPDATE, or DELETE) operations on one or more replication target tables. It occurs when the Receiver receives an XLog.
    
-   **Change Operation:**  
    This term indicates an INSERT, UPDATE, or DELETE DML operation. This term is used to distinguish these operations from SELECT operations (which do not change the contents of a database).
    
-   **Replication:**  
    This term indicates the concept and action of replicating, rather than a concrete object or entity.

-   **Synchronization:**  
    "Synchronization" is a unidirectional operation in which all data in the replication target tables or partitions on the local server are inserted into the corresponding tables or partitions on the remote server. If any data conflict occurs on the remote server during synchronization, conflict resolution will be applied on the remote server. It is performed by executing the ALTER REPLICATION DDL statement with either the SYNC or SYNC ONLY keyword.
    
-   **Replication Gap:**  
    Conceptually, the replication gap is an indicator of how far the replication process has fallen behind the current state of the database. In quantitative terms, it is the difference between the sequence number (not XSN) of the most recent redo log and the sequence number of the redo log for which the corresponding XLog is currently being sent.
    
-   **Replication Manager:**  
    This is the Altibase module that starts and stops the replication Sender and Receiver.

-   **Replication Object:**  
    This is an object created with the CREATE REPLICATION statement. It forms a replication pair with a counterpart replication object on another node. 
    
-   **Replication Pair:**  
    This is a pair of corresponding replication objects having the same name, one residing on each of the two different nodes. 

-   **Replication Target Column:**  
    This is a column that exists in corresponding replication target tables on local and remote servers. Replication target columns cannot be explicitly designated; rather, they are determined by the structure of the corresponding replication target tables.
    
-   **Replication Target Table:**  
    This is a table that is designated, using the CREATE REPLICATION or ALTER REPLICATION statement, to be replicated between corresponding replication nodes. 
    
-   **Replication Target Patition:**  
    This is a table parition that id designated, using the CREATE REPLICATION or ALTER REPLICATION statement, to be replicated corresponding replication nodes.
    
-   **EAGER Mode:**  
    This is one of two available replication modes which prioritizes data consistency over performance. In this mode, a transaction is not committed on the local server until the local server receives a message from the remote server stating that the task has been performed and the transaction replayed on the remote server.
    
-   **LAZY Mode:**  
    This is the other of the two available replication modes which prioritizes performance over data consistency. In this mode, a transaction is committed on the local server without waiting for confirmation from the remote server.
    
-   **Parallel Replication:**  
    This is the use of multiple Sender and Receiver threads to perform replication in EAGER mode. This is not to be confused with parallel synchronization.
    
-   **Parallel Synchronization:**  
    This is the use of multiple Sender and Receiver threads to accomplish a synchronization task (using "ALTER REPLICATION ... SYN" or "ALTER REPLICATION ... SYNC ONLY). This is not be confused with parallel replication.

#### How to Perform Replication in Altibase

Replication is conducted in this way: the local server sends information of changes made to the database contents to the remote server, and then the remost server makes the same changes to its database.

Thus,the local and remote servers operate additional threads (apart from the service threads) that are necessary for managing replication. 

The replication Sender thread on the local server sends information of changes made to the database contents to the remote server, and then the replication Receiver thread on the remote server makes the same changes to the database on the remote server. 

Also, the replication Sender and Receiver threads automatically detect whether or not the corresponding servers shut down normally, and perform the corresponding operation.

Figure [1-1] shows various ways in which replication is supported.

In Altibase, the best of these ways is to transform redo logs into a directly executable logical structure to maximize performance and flexibility.

![](media/Replication/d6ea6c6febc5fb2ec5e4702e8e7d90f0.png)

Figure 1-1 A Review of Replication Methods

1.  Performing replication using a client application  
  
    In this case, it downgrades performance and renders data consistency.
    
    If replication is performed by issuing commands in an application, the repeated execution of the same query or transaciton execution order can disrupt data consistency as Altibase performs replication by replaying logs.

2. Sending queries  
    This method increases the load on the QP (Query Processor) and renders validation difficult due to data collisions.

3. Sending execution plans  
    This method increases the communication load due to the increased volume of transmissions. 

4. Converting logs into query statements  
    This method increases high conversion and query processing costs. 

5. Converting logs directly into a form that can be executed  
    This method requires high conversion cost but improves replication performance.

6. Transmitting logs and performing log-based recovery  
    This method is fast but cannot be used in an "Active-Active" environemnt (one in which both servers are providing service).

#### Choosing a Replication Server

To perform replication in Altibase, the database character sets and the national sets must be the same on both the local and remote servers. 

The character sets can be checked by querying the V$NLS_PARAMETERS performance view.

#### Choosing Replication Targets

Altibase uses object names to specify replication targets. 

When creating a replication object, the names of users and tables that are to be designated as replication targets must be directly specified. To replicate only a particular partition of a partitioned table, the name of the partition, the name of the table which contains the partition and the name of the owner of the table must be directly specified. Additionally, only columns that have the same names on both the local and remote servers at the time of replication can be replication targets.

The replication target columns can be checked by querying the V$REPRECEIVER_COLUMN performance view.

#### Replication Mode

In Altibase, replication can run in one of the following modes:

* LAZY Mode
* Eager Mode

In Table 1-1, each replication mode has different characteristics in terms of performance, the possibility of delayed replication, and the level of data consistency, as shown in the table below. 

| Mode  | Performance | Delayed Replication | Data Consistency |
| ----- | ----------- | ------------------- | ---------------- |
| LAZY  | High        | Possible            | Low              |
| EAGER | Medium      | Impossible          | High             |

##### LAZY Mode

In LAZY mode, when a transaction occurs on a local server ("Master Transaction") and a DML statement is executed on a replication target table, the Sender thread collects logs recorded by the Master Transaction, converts them into XLOGs and sends them out. The Receiver thread on the remote server receives these XLOGs and commits the replication transactions to its database.

Thus, the transcations do no not influence one another and the performance of the local server is excellent because the master transaction and replication transaction occur separately.

However, since the Sender thread always tracks the master transaction, replication may not always be completely up-to-date on very busy sites.

##### EAGER Mode

In EAGER mode, when a master transaction occurs on a local server, the local server commits the transaction only after it has received confirmation that all of the corresponding logs have been properly applied on the remote server. The remote server commits the replication transaction at the same time. In other words, replication in EAGER mode is a synchronization method[^1].

[^1]: Transaction Synchronization: Even if a master transaction is successfully performed on a local server, if a replication conflict occurs on a remote server, it will be impossible to commit the master transaction on the local server. In such cases, the user must explicitly roll back the transaction to execute the next transaction. If the transaction is not rolled back, it will be impossible to apply any changes because a transaction that cannot be committed is continually pending. Under conditions in which the local server is internally required to commit a transaction (e.g., when running in Autocommit mode or when a session is terminated), the conflict causes the master transaction that could not be committed to be automatically rolled back. As a result, the master transaction that experienced the conflict and the replication transaction are both rolled back, thereby 

The advantage of EAGER mode is that because it synchronizes transactions, it allows replication to occur in parallel. Therefore, when replication is performed in EAGER mode, multiple sender threads replicate concurrently. The number of parallel threads can be configured using the REPLICATION_EAGER_PARALLEL_FACTOR property.

Although there may be a slight performance degradation due to transaction synchronization, EAGER mode avoids the replication backlog that can occur in high-transaction environments under LAZY mode.

Before using EAGER mode replication, please refer to the [Replication Constraints in EAGER Mode](#replication-constraints-in-eager-mode).

#### Replication of Partitioned Tables 

As shown in the following figure, a particular partition of a partitioned table can be specified and replicated.

![](media/Replication/image11.gif)

[Figure 1-2] The Structure of a Replicated Partitioned Table

#### Replication and DDL (Data Definition Language) clone

In Altibase, replication performs based on the column name of the table to be replicated, so that it can be replciated even for tables with different table schemas. For this reason, it allows some DDL to change the schema even if the table is subject to be replicated.

When the table schema is changed by executing DDL, only the data of the column with the same name in both nodes is replicated, and the column in the other name or only one side is not replicated. 

If the table schema is replicated in a different state, performance will be deteriorated. Therefore, if the table schema is changed by performing DDL, it is advantageous to perform the same DDL so that both nodes have the same schema.

DDL operation on the table included in the replication can be performed or replicated on a single node based on the user's choice. In the case of replication DDL, the DDL is replicated after synchronizing all the replication data.

When replication DDL, DML except SELECT cannot be performed while synchronizing the replication data, so use it with caution when replicated is performed.

#### Extra Features

Altibase provides the following additional features. A detaield description of how to use the add-ons and limitations is given in the section on Extra Features.

-   Recovery Option  
    : If experiencing abnormal server termination during the replication, data recovery option is available for preventing data inconsistency between servers by replications.
    
-   Replication Gapless Option  
    : The replication gapless option resolves replication gaps.

-   Parallel Receiver Applier Option  
    : This option allows receivers to apply XLog received from the sender in parallel.

-   Replication Transaction Grouping Option  
    : This option sends logs to a sender thread by grouping multiple transaction to a single transaction when replication gap occurs.
    
-   Meta Logging Option  
    
    : This option records the sender meta and Restart SN information into files.
    
-   Offline Option

    : The function that retrieves the untransmitted logs from the Active server and applies the change transactions to the remote server.

> #### Considerations
>
> Tables or partitions are items which can be replicated in Altibase and the corresponding replication target items on both servers must be the same type. Thus, a table can be replicated to a table and a partition can be replicated to a partition, but a crossover replication is impossible.
> 
> When dropping a replication target item from a replication object, the item must be specified exactly as it was added. For example, even if every partition of a partitioned table is added as replication targets, it is impossible to specify a partitioned table and exclude it from being a replication target; however, it is possible to specify each partition separately for exclusion.

# 2. Managing Replication

This chapter explains the replication steps and how to use Altibase replication functions for various faults and errors that can occur while performing replication.

### Replication Procedures

![](media/Replication/Replication_eng.1.6.1.jpg)

[Figure 2-1] Replication Procedures

1.  Choose the replication target servers  
    The database character sets and the national character sets of both servers must be the same. 
    
2.  Choose the tables or partitions to be replicated  
    Every table to be replicated must have a primary key.

3.  Create a replication object using the CREATE REPLICATION statement  
    The replication object must have the same name in both databases.
    
4. Start replication using the ALTER REPLICATION statement 

    When replication is started, the local server creates a replication Sender thread and this thread connects to a replication manager on the remote server. At this time, the replication manager on the remote server generates a repliation Receiver thread.

5.  The replication service is started.

### Troubleshooting

-   Abnormal local or remote server shutdown
-   Communication interruption between local and remote servers
-   Service line failure

#### Abnormal Local or Remote Server Shutdown

![](media/Replication/Replication_eng.1.7.1.jpg)

[Figure 2-2] Replication in the Event of Server Failure

##### Server A abnormally terminates

The Receiver thread on Server B terminates and the Sender thread on Server B attempts to connect to Server A at regular intervals (e.g., every 60 seconds).

##### Server A restarts (the Sender thread calls the Receiver thread on the remote server)

1.   Server A’s Sender thread automatically starts and performs replication with Server B. 
2.  Server B’s Sender thread starts Server A’s replication Receiver thread and it performs replication. 
3.  Server B’s Sender thread starts Server A’s Receiver thread. 
4.  Server A’s Sender thread starts Server B’s Receiver and it performs replication. 

#### Communication Interruption Between Local and Remote Servers

![](media/Replication/Replication_eng.1.7.2.jpg)

[Figure 2-3] Replication in Response to Communication Failure with Remote Server

##### The local and remote servers fail to communicate0

1.  The Receiver threads on Server A and B roll back and terminate uncommitted transactions
  
2.  The Sender threads on Server A and B record the Restart SN and attempt to connect to the corresponding servers every 60 seconds.

##### Connection is restored

1.  The Sender threads on Server A and B wake up the receiver threads on the corresponding servers and perform replication by transmitting all XLOGs, starting with the XLOG corresponding to the Redo Log having the Restart SN.
  
2.  Receiver threads on Server A and B are created in response to connection requests from the Sender threads on corresponding servers, and perform replication.

#### Service Line Failure

![](media/Replication/Replication_eng.1.7.3.jpg)

[Figure 2-4] Replication in the Event of Service Line Failure

##### • Primary line is disconnected

1.  Server B provides service with a backup line.

##### Primary Line is restored

1.  Once the primary line is restored, Server A provides service.

2.  Even if the primary line is down, Server B can still send task contents to Server A with the Altibase replication functionality.

### Conflict Resolution

A ”data conflict” occurs when the master transaction makes data changes, but the replication transaction cannot apply the changes due to duplicate primary keys or constraints.

For Deferred Replication, the best way to avoid data conflicts is to have different update data sets per database.

There are three types of data conflicts:

##### INSERT Conflicts

-   An INSERT conflict occurs if the replication transaction tries to insert data that has the same primary key as an existing record.

-   If the replication transaction tries to insert data into a table that is already locked by another local transaction, the replication transaction needs to wait to acquire a lock. An INSERT conflict occurs due to lock timeout. 
  
-   An INSERT conflict occurs if the replication transaction tries to insert a duplicate value into a primary key column. 

##### UPDATE Conflicts

-   An UPDATE conflict occurs if the replication transaction tries to update a record with a nonexistent primary key. 

-   An UPDATE conflict occurs if the replication transaction tries to update a record whose data is different from the record’s before image (i.e. data prior to changes ) updated by the master transaction. 
  
-   An UPDATE conflict occurs if a duplicate key value is created by an update operation. 

##### DELETE Conflicts

-   A DELETE conflict occurs if the replication transaction tries to delete a record that has a nonexistent primary key.
  
-   If the replication transaction tries to delete a record that is already locked by the local transaction, the replication transaction needs to wait to acquire a lock. A DELETE conflict occurs due to lock timeout.

Unlike distributed DBMSs that use the 2-Phase Commit (2-PC) or 3-Phase Commit (3-PC) protocols, the replication functionality cannot guarantee data consistency against conflicts for commercial DBMSs. Contrariwise, 2-PC/3-PC have performance degradation issues and additional measures are required for system or network failure.

As a result, commercial DBMSs mainly use deferred (asynchronous) replication to alleviate the constraints on data consistency and maintain solid performance. 

#### Conflict Resolution

“Conflict resolution” refers to a variety of methods for eliminating data conflicts. Deferred Replication does not offer a perfect solution to data conflicts. Once a conflict occurs, it is merely resolved by synchronizing the data on the database servers. Altibase provides the following conflict resolution methods to resolve data conflicts:

* User-Oriented Scheme 
* Master-Slave Scheme 
* Timestamp-Based Scheme

Altibase performs the following operations for the above methods:

-   Synchronizes a server’s data with another server.

-   Logs information about conflicts for issue tracking.

However, LOB columns are excluded from conflict resolution. LOB columns cannot detect data conflict because they neither log before images nor define primary or unique keys. 

The policies for each conflict situations are provided in detail below. 

Note: For more detailed description of the CREATE REPLICATION command, please refer to the description of the CREATE REPLICATION statement.

#### User-Oriented Scheme

##### Syntax

```
CREATE REPLICATION replication_name
WITH 'remote_host_ip', remote_host_port_no 
FROM user_name.table_name TO user_name.table_name
FROM user_name.table_name TO user_name.table_name,
… 
FROM user_name.table_name TO user_name.table_name;
```

##### Description

-   INSERT Conflict  
    If an INSERT conflict occurs, the INSERT statement fails and a conflict error message is output to altibase_rp.log.  
    Use the REPLICATION_INSERT_REPLACE property to set the conflict resolution policy for an INSERT conflict that arises due to trying to insert data having the same primary key as an existing record.  
    REPLICATION_INSERT_REPLACE=1: Delete and insert 
    REPLICATION_INSERT_REPLACE=0: Either does not delete or insert; outputs an error message
    
-   UPDATE Conflict  
    If an UPDATE conflict occurs, the UPDATE statement fails and a conflict error message is output to altibase_rp.log  
    Use the REPLICATION_UPDATE_REPLACE property to set the conflict resoultion policy for an UPDATE conflict that arises due to trying to update data with a different before image or update data with a nonexistent primary key.  
    For example, the following policies can be used when there is a data of the value 10 and the replication transaction tries to update that value from 20 to 30.  
    REPLICATION_UPDATE_REPLACE=1 : Update  
    REPLICATION_UPDATE_REPLACE=0 : Does not update; outputs a conflict error message
    
-   DELETE Conflict  
    If a DELETE conflicts occurs, the DELETE statement fails and a conflict error message is written to altibase_rp.log.

##### Summary

-   The user determine the conflict resolution policy on a case-by-case basis. 

-   The altiComp utility is provided as a solution for with data inconsistency. For more detailed information, please refer to the *Utilities Manual.* 

#### Master-Slave Scheme

##### Syntax

```
CREATE REPLICATION replication_name {as master|as slave}
WITH 'remote_host_ip', remote_host_ port_no
FROM user_name.table_name TO user_name.table_name,
FROM user_name.table_name TO user_name.table_name,
… 
FROM user_name.table_name TO user_name.table_name;
```

##### Description

- Specify ”MASTER” or “SLAVE” in the command to specify whether the server is the Master or Slave. On omission, the value specified by the REPLICATION_INSERT_REPLACE or REPLICATION_UPDATE_REPLACE property is used.
  
- The user can check whether a server is the Master or Slave from the CONFLICT_RESOLUTION column in the SYS_REPLICATIONS_ meta table. *
  
- 0 = not specified 
  
- 1 = Master; 
  
- 2 = Slave
  
- The handshake[^2] is only successful if the CONFLICT_RESOLUTION column has the following values: 0 with 0, 1 with 2, and 2 with 1. Any other combinations will fail. If one server is specified as the Master but the other server is omitted , the following error will be output when replication starts: 
  
  [^2]: Handshaking is the process of checking whether the other server is alive and whether the information about the objects to be replicated between the local server and the remote server matches before replication starts.

```
iSQL> ALTER REPLICATION rep1 START
[ERR-6100D : [Sender] Failed to handshake with the peer server (Master/Slave conflict resolution not allowed [1:0])]
```

##### Master/Slave Replication Conflict Handling Method

###### Operating as Master

-   INSERT conflict: Not committed. 
-   UPDATE conflict: Not committed. 
-   DELETE conflict: Not committed. 
-   Other: XLOG transferred from the Slave is processed as usual.

###### Operating as Slave

-   INSERT conflict:  If an insert conflict occurs because an attempt was made to insert data having the same primary key as an existing record, the existing record is deleted and a new record is added.  
    If an insert conflict occurs for any other reason, the INSERT statement fails, and a conflict error message is recorded in altibase_rp.log.
    
-   UPDATE conflict:  If an update conflict occurs because an attempt was made to update a record having a value different from the “Before Image” value on another database server, from which data for replication are propagated, the conflict is ignored, and the UPDATE statement succeeds despite the conflict.  
    If an update conflict occurs for any other reason, the UPDATE statement fails, and a conflict error message is recorded in altibase_rp.log.
-   DELETE conflict:  If a delete conflict occurs because no record having that primary key exists, the DELETE statement fails, and a conflict error message is not recorded in altibase_rp.log.  
    If a delete conflict occurs for any other reason, the DELETE statement fails, and a conflict error message is recorded in altibase_rp.log.
-   Other: The XLOG transferred from the Master is processed as usual.

##### Example

Suppose that the IP address and replication port number of the local server are 192.168.1.60 and 25524, and that the IP address and replication port number of the remote server are 192.168.1.12 and 35524, that there is a master-slave relationship between the local and remote servers, and that a table called employees and one called departments are replication target tables. In this situation, replication is specified as follows:

-   Local Server (IP: 192.168.1.60)

```
iSQL> CREATE REPLICATION rep1 AS MASTER
    WITH '192.168.1.12', 35524
    FROM sys.employees TO sys.employees,
    FROM sys.departments TO sys.departments;
Create success.
```

-   Remote Server (IP: 192.168.1.12)

```
iSQL> CREATE REPLICATION rep1 AS SLAVE
    WITH '192.168.1.60', 25524
    FROM sys.employees TO sys.employees,
    FROM sys.departments TO sys.departments;
Create success.
```

Whether a server is a Master or Slave can be determined by checking the CONFLICT_RESOLUTION field, which is located in the SYS_REPLICATIONS_ meta table. (0 = not specified; 1 = Master; 2 = Slave)

```
iSQL> SELECT replication_name, conflict_resolution FROM system_.sys_replications_;
REPLICATION_NAME    CONFLICT_RESOLUTION
---------------------------------------------------------------------------
REP1                   1
1 row selected.
```

#### Timestamp-based Scheme

##### Syntax

```
CREATE REPLICATION replication_name
WITH ‘remote_host_ip’, remote_host_port_no 
FROM user_name.table_name TO user_name.table_name,
FROM user_name.table_name TO user_name.table_name,
… 
FROM user_name.table_name TO user_name.table_name;
```

##### Description

The Timestamp-Based Scheme is provided to ensure that both servers have the same data in an Active-Active replication environment.

The following restrictions apply when using the Timestamp-Based Scheme:

-   Every table must contain a TIMESTAMP column.

-   The REPLICATION_TIMESTAMP_RESOLUTION property must be set to 1.

Because Altibase supports the Timestamp-Based Scheme on the basis of tables, even if a replication target table has a TIMESTAMP column, if the value of the REPLICATION_TIMESTAMP_RESOLUTION property for that table has been set to 0, a conventional conflict resolution scheme will be used. 

Supposing for example that a user wishes to replicate a table called "foo" and another called "bar" between two servers, if the REPLICATION_TIMESTAMP_RESOLUTION property is set to 1 for the "foo" table, the Timestamp-Based Scheme will be used for that table, whereas a conventional conflict resolution scheme will be used for the "bar" table.

```
CREATE TABLE foo (a DOUBLE PRIMARY KEY, b TIMESTAMP);
CREATE TABLE bar (a DOUBLE PRIMARY KEY, b CHAR(3));
CREATE REPLICATION rep WITH ’127.0.0.1’, 30300 FROM sys.foo TO sys.foo, FROM sys.bar TO sys.bar;
```

##### Timestamp-based Replication Processing Method

Altibase supports the Timestamp-Based Scheme only for INSERT and UPDATE operations.

###### INSERT

1.  If data to be inserted have the same key as existing data, the timestamp value of the After-Image of the data is compared with that of the existing data.
  
2.  If the TIMESTAMP value of the After-Image of the data is equal to or greater (i.e. more recent) than that of the existing data, the existing data are deleted, and new data, having the value of the After-Image of the data, are added.

###### UPDATE

1.  The TIMESTAMP value of the After-Image of the data is compared with that of the data to be updated.
  
2.  If the TIMESTAMP value of the After-Image of the data is equal to or greater (more recent) than that of the existing data, the data are updated with the After-Image of the data

3.  When UPDATE is performed, the TIMESTAMP value in the After-Image of the data is kept. In other words, independent system time values are not used.

> ##### Restrictions
>
> -   When a TIMESTAMP column is added to a table, 8 additional bytes of storage space are needed per record. 
>   
>-   If the time is set differently on the two servers to be replicated, database inconsistencies can result. 
> 

### Eager Replication Failback

This section examines how the data of both servers are synchronized and then failback when a node fails in the replication environment of eager mode.

To configure a replication environment in eager mode, replication of both servers in eager mode must be created and started. In addition, in order to failback in a replication environment of the eager mode, replication must be operated in the eager mode even in the failback environment (recovery).

#### Incremental Sync

In the replication environment in Eager mode, a failure (equipment issue or Altibase server failure) may occur on a Server A without a commit log written on one server (Server A) and the commit log is not sent to the other server (Server B). In this case, Server A returns an error to the application that executed the transaction commit, and Server B will roll back the transaction because it does not receive the commit log. Then, application will fail over and continue working on Server B. AS a result, there may be a situation in which data in the same record does not match on Server A and Server B.

Since this data affects the replication operation in the future, a failback process for inconsistent data of both nodes is required. This is called 'incremental sync', a data synchronization operation for removing inconsistencies caused by replication node failures of EAGER mode. Targets of this operation are records with any possibility of committed on only one node. Incremental Sync analyzes data that can be different from the other node, requests and synchronizes those missing transaction logs. 

When Server A comes back online, it is determined as the value of the REMOTE_FAULT_DETECT_TIME column in the SYS_REPLICATIONS meta tables of both servers (when the failure of the other nodes is detected), to become master or slave respectively. That is, the server with later value becomes the master. In this case, Server B will be the master server. Once the master and the slave are determined, the replication sender of the slave (Server A) analyzes its transaction log from the restart SN (sequence number) and determines the data that have not been sent to the other server (i.e., may be different from the master), and import the data from the master and perform the synchronization. The master's replication sender sends the data requested by the slave. That is, the replication senders of both servers operate as master and slave. 

Thus, in order to increment synchronization to complete successfully, neither of the replications of both servers should be stopped.

Then, replication sender of Server A updates the restart SN (sequence number) to the latest. This is to prevent the replication sender of Server A from retransmitting the data that are already syncrhonized in the above process.

Incremental Sync can be enabled or disabled by adjusting the REPLICATION_FAILBACK_INCREMENTAL_SYSN property value, which must be set to the same value on both nodes' server.

#### Normal Sync

After the server completes or skips the incremental sync, before the Eager mode replication starts normally, it synchronizes the data from the transaction log that failed to transfer from Server B to Server A during the failure. This synchronization is called normal sync. When transmitting a log that could not be transmitted could be transmitted due to a failure, replication switches to the Lazy mode, and when all the logs are transmitted and there is no replication gap, replication starts by switching back to the Eager mode.

When the REPLICATION_FAILBACK_INCREMENTAL_SYNC property value is set to 1, normal synchronization will be performed after the above incremental sync. Otherwise, incremental sync will be skipped and normal synchronization will be performed immediately. 

### Parallel Replication

Parallel replication indicates using multiple sending and receiving threads when executing the replication. 

Altibase supports the following parallel replication based upon the replication mode:

-   Lazy mode: This is one of the additional features which allows receiver parallel replication.
-   Eager mode: This allows sending parallel replication by controlling properties

In the eager mode, the parallel replication is used by controlling REPLICATION_EAGER_PARALLEL_FACTOR property in order to manage multiple sending threads.

In case of replication in the eager mode, it is available to replicate a transaction unit since commit execution is possible if nodes in both sides are read. Altibase materializes the parallel replication with multiple replication sender threads so that each thread can process one transaction. Also, this type of parallel replication offers much enhanced replication performance with rapid speed that that of the conventional synchronous replication.

The parallel replication method in lazy mode is described in the Extra Features section.

> #### Note*: 
>
> If using the parallel replication, there might be an impossible situation to commit due to reversed transaction sequence in the process of replicating. Thus, the application program should implement logic in order to overtly execute a rollback if a commit failure is returned when using the parallel replication.

### Performance View related to Replication

The following performance views are provided to monitor replication progress. For more information on performance views, see the General Reference.

-   V\$REPEXEC

-   V\$REPGAP

-   V\$REPGAP_PARALLEL

-   V\$REPLOGBUFFER

-   V\$REPOFFLINE_STATUS

-   V\$REPRECEIVER

-   V\$REPRECEIVER_COLUMN

-   V\$REPRECEIVER_PARALLEL

-   V\$REPRECEIVER_STATISTICS

-   V\$REPRECEIVER_TRANSTBL

-   V\$REPRECEIVER_TRANSTBL_PARALLEL

-   V\$REPRECOVERY

-   V\$REPSENDER

-   V\$REPSENDER_PARALLEL

-   V\$REPSENDER_STATISTICS

-   V\$REPSENDER_TRANSTBL

-   V\$REPSENDER_TRANSTBL_PARALLEL

-   V\$REPSYNC

# 3. Deploying Replication

### Considerations 

There are several conditions apply when establishing replication. If these conditions are not met, replication cannot be deployed.

#### Prerequisites

-   If a conflict occurs during an INSERT, UPDATE, or DELETE operation, the operation is skipped, and a message is written to an error file. 
-   If an error occurs during replication, partial rollback is performed. For example, if a duplicate row is found while inserting rows into a table, only the insertion of the duplicate row is canceled, while the remainder of the task is completed as usual. 
-   Replication is much slower than the main data provision service

#### Data Constraints

- The table to be replicated must have a primary key.

- The primary key of the table to be replicated must not be modified.

- If the column types, NOT NULL constraints, CHECK constraints, unique key indexes, or function-based indexes of the replicated table differ between the two servers, and `REPLICATION_SQL_APPLY_ENABLE` is set to 1, the replication will operate in [SQL Apply Mode](#appendix-c-sql-apply-mode), which may result in reduced performance.

#### Connection Constraints

-    The maximum number of replication connections possible from one Altibase database is determined by the REPLICATION_MAX_COUNT property. 
-   The database character sets and the national character sets must be the same on both servers in order for replication to be possible. Which character set is currently in use can be checked by viewing the values of NLS_CHARACTERSET and NLS_NCHAR_CHARACTERSET in the V$NLS_PARAMETERS performance view.

#### Replication Target Column Constraints

-   When an INSERT transaction is replicated, columns that are not replication targets will be filled with NULL values.
  
-   When configuring unique indexes and function-based indexes of a replicated column and a non-replicated column, it operates in the SQL apply mode.

#### Replication Constraints in EAGER Mode

The following constraints apply to replication in EAGER mode. 

-   To ensure data consistency, replication in EAGER mode is not recommended for more than three nodes.

-   Data is not synchronized unless replication is performed in EAGER mode on both the remote and local servers.
  
-   If a network failure occurs while replication is being performed in EAGER mode (and even if the server manages to service properly), data consistency cannot be guaranteed. This is because when a network failure occurs, each node interprets the failure as an error on the other node, and both nodes update data. 
  
-   A table can only be replicated as a single corresponding table when replication is performed in EAGER mode. If a table is replicated into two or more tables in EAGER mode, data will be inconsistent and incremental synchronization will fail. 
  
-   Servers on which replication is being performed must have their time synchronized. If an error occurs and the time has not been synchronized, replication can be defective due to the time difference at error detection. 
  
-   Data can be lost if the server abnormally terminates before a committed XLog is applied on disk in EAGER mode. To prevent data loss, specify the recovery option or adjust the values for commit-related properties (COMMIT_WRITE_WAIT_MODE, REPLICATION_COMMIT_WRITE_WAIT_MODE, and REPLICATION_SYNC_LOG)
  
-   SQL apply mode is not available for replication in the EAGER mode.

#### Partitioned Table Constraints

The following conditions must be met in order to successfully replicate partitioned tables.

-   The partitioning method must be the same on both the remote server and the local server.

-   For range or list partitions, the partitioning conditions must be the same. If only some partitions are to be replicated, the constraints on only those partitions need to be the same. The same applies to default partitions. 
  
-   For hash partitions, the number of partitions must be the same.

#### Constraints on Using Replication for Data Recovery

-   In order to use replication to perform data recovery, the following restrictions apply: 
    1. If both the local server and the remote server shut down abnormally, recovery using replication will not be possible. 
    2. Conflicting data cannot be recovered. 
    3. A single table cannot be recovered using two or more replication objects. 
    4. If transactions that have not been transferred are lost, the data cannot be recovered.

#### Additional Considerations when Using Replication for Data Recovery

-   If different update operations are performed on the same record on two replicated systems in an Active-Active replication environment, data may be mismatched between the systems. 
-   If a network error occurs or replication is stopped according to the setting of the REPLICATION_RECOVERY_MAX_TIME property by the user, data might not be recovered.

### CREATE REPLICATION

Before starting replication, corresponding replication objects must be created on two servers first.

#### Syntax

```
CREATE [LAZY|EAGER] REPLICATION replication_name 
[FOR ANALYSIS | FOR PROPAGABLE LOGGING | FOR PROPAGATION | FOR ANALYSIS PROPAGATION] 
[AS MASTER|AS SLAVE] 
[OPTIONS options_name [option_name ... ] ] 
WITH { ‘remote_host_ip’, remote_host_ port_no [USING conn_type [ib_latency]]} 
...
FROM user_name.table_name [PARTITION partition_name] TO user_name.table_name [PARTITION partition_name]
[,FROM user_name.table_name [PARTITION partition_name] TO user_name.table_name [PARTITION partition_name]
...;
```

#### Prerequisites

Only the SYS user can execute replication-related statements.

#### Description

Before replication can be performed, a so-called "replication pair", comprising of a pair of replication objects between which a connection is established, must be set up.

Replication is conducted on a table-by-table or a partition-by-partition basis. Tables or partitions are matched one-to-one.

When creating a replication object, one of the LAZY and EAGER modes can be selected as the default mode. If the replication mode is not specified for a session, this default mode will be used. If no default mode is specified, replication will be performed in LAZY mode.

- ***replication_name***  
  This specifies the name of the replication object to be created. The same name must be used on both the local server and the remote server.
  
- ***FOR ANALYSIS \| FOR ANALYSIS PROPAGATION***  
  This creates the Xlog Sender. For more detailed information about properties, please refer to the Log Analyzer User’s Manual.
  
- ***FOR PROPAGABLE LOGGING \| FOR PROPAGATION***  
  Replication receiver writes the logs received with FOR PROPAGABLE LOGGING. FOR PROPAGATION is used to send propagable logs to other target server. 
  
  This function cannot be used with recovery option.
  
- ***as master or as slave***  
  This specifies whether the server is the Master or the Slave. If not specified, the value specified using the REPLICATION_INSERT_REPLACE or REPLICATION_UPDATE_REPLACE property will be used. When attempting to perform handshaking, the following combinations of values will be successful: 0 with 0, 1 with 2, and 2 with 1. Other combinations will fail. (0 = not set; 1 = Master; 2 = Slave)
  
- ***remote_host_ip***  
  This is the IP address of the remote server.

- ***remote_host_port_no***  
  This is the port number at which the remote server Receiver thread listens. More specifically, this is the port number specified in REPLICATION_PORT_NO in the altibase.properties file on the remote server.
  
- ***conn_type***  
  This is the communication method with a remote server (TCP/InfiniBand). The default value is TCP.

- ***ib_latency***  
  This is the RDMA_LATENCY option value for rsocket. It can be only inserted when conn_type is IB

- ***user_name***  
  This is the name of the owner of the table to be replicated.

- ***table_name***  
  This is the name of the table to be replicated.

- ***partition_name***  
  This is the name of the partition to be replicated.

- ***option_name***  
  This is the name of the additional functions pertaining to the replication object. For more detailed information, please refer to Extra Features

#### Error Codes

Please refer to the Altibase *Error Message Reference*.

#### Example

Suppose that the IP address and port number of the local server are 192.168.1.60 and 25524, and that the IP address and port number of the remote server are 192.168.1.12 and 35524. To replicate a table called employees and one called departments between the two servers, the required replication definition would be as follows: 

-   Local server (IP: 192.168.1.60)

```
iSQL> CREATE REPLICATION rep1
    WITH '192.168.1.12', 35524
    FROM sys.employees TO sys.employees,
    FROM sys.departments TO sys.departments;
Create success.
```

-   Remote Server (IP: 192.168.1.12)

```
iSQL> CREATE REPLICATION rep1
    WITH '192.168.1.60', 25524
    FROM sys.employees TO sys.employees,
    FROM sys.departments TO sys.departments;
Create success.
```

### Starting, Stopping and Modifying Replication using “ALTER REPLICATION”

#### Syntax

```
ALTER REPLICATION replication_name 
SYNC [PARALLEL parallel_factor] 
[TABLE user_name.table_name [PARTITION partition_name], … , user_name.table_name [PARTITION partition_name]];

ALTER REPLICATION replication_name 
SYNC ONLY [PARALLEL parallel_factor] 
[TABLE user_name.table_name [PARTITION partition_name], … , user_name.table_name [PARTITION partition_name]];

ALTER REPLICATION replication_name START [RETRY];

ALTER REPLICATION replication_name QUICKSTART [RETRY];

ALTER REPLICATION replication_name STOP; 

ALTER REPLICATION replication_name RESET;

ALTER REPLICATION replication_name DROP TABLE 
FROM user_name.table_name [PARTITION partition_name] TO user_name.table_name [PARTITION partition_name];

ALTER REPLICATION replication_name ADD TABLE 
FROM user_name.table_name [PARTITION partition_name] TO user_name.table_name [PARTITION partition_name]

ALTER REPLICATION replication_name FLUSH [ALL] [WAIT timeout_sec];
```

#### Prerequisites

Only the SYS user can execute replication-related statements.

#### Description

-   SYNC  
    After all of the records in the table to be replicated have been transmitted from the local server to the remote server, replication starts from the current position in the log. In order to prevent another transaction from changing data in the table on which synchronization is to be performed right at the time of determination of the log from which replication will start after synchronization, the Replication Sender Thread obtains an S Lock on the table on which synchronization is to be performed for a short time before synchronization. Therefore, if a synchronization attempt is made while another transaction is updating data in the table to be synchronized, the Replication Sender Thread will wait for the amount of time specified in the REPLICATION_SYNC_LOCK_TIMEOUT property, and will then start replication at the time at which the change transaction ends. If the change transaction is not completed within the amount of time specified in the REPLICATION_SYNC_LOCK_TIMEOUT property, synchronization will fail. If, during synchronization, records on the local server are found to have the same primary key values as records on the remote server, any conflicts are eliminated according to the rules for conflict resolution.
    
-   TABLE  
    This specifies the table that is the target for SYNC replication.

-   PARTITION  
    This specifies the partition that is the target for SYNC replication. 

-   PARALLEL  
    *Parallel_factor* may be omitted, in which case a value of 1 is used by default. The maximum possible value of *parallel_factor* is the number of CPUs * 2. If it is set higher than this number, the maximum number of threads that can be created is still equal to the number of CPUs * 2. If it is set to 0 or a negative number, an error message results. 
    
-   SYNC ONLY  
    All records in replication target tables are sent from the local server to the remote server. (In this case the Sender thread is not created.) If the same records exist on both the local server and the remote server, sources of conflict are eliminated according to the rules for conflict resolution. 
    
    Because only a single thread is responsible for handling SYNC or SYNC ONLY on disk tables, when some of the tables on which SYNC replication is to be performed are disk tables, setting *parallel_factor* higher than the number of disk tables confers a performance advantage. 
    
-   START  
    Replication will start from the time point of the most recent replication.

-   QUICKSTART  
    Replication will start from the current position in the log.

-   START/QUICKSTART RETRY  
    When starting or quickstarting replication with the RETRY option, even if handshaking fails, a Sender Thread is created on the local server. Afterwards, once handshaking between the local server and the remote server is successful, replication starts. 
    
    iSQL shows a success message even if the first handshake attempt fails. Therefore, the user must check the result of execution of this command by checking the trace logs or the V$REPSENDER performance view. 
    
    When starting replication without the RETRY option, if the first handshake attempt fails, an error is raised and execution is stopped.
    
-   STOP  
    This stops replication. If a SYNC task is stopped, the transmission of all data to be replicated to the remote server cannot be guaranteed. If a SYNC replication that is underway is stopped, in order to perform SYNC again, all records must be deleted from all replication target tables, and then the SYNC is performed again.
    
-   RESET  
    This command resets replication information (such as the restart SN (Sequence Number)). It can only be executed while replication is stopped, and can be used instead of executing DROP REPLICATION followed by CREATE REPLICATION.
    
-   DROP TABLE 
    
    A specific table or partition is excluded from the replication target.
    If the primary transaction log or table metadata log of the target table is within a replication gap at the time `DROP TABLE` is executed, the replication gap will be skipped, which may result in data inconsistency. 
    
-   ADD TABLE  
    This command adds a table or a partition to a replication object. It can only be executed while replication is stopped.
    
-   FLUSH  
    The current session waits for the number of seconds specified by *timeout_sec* so that the replication Sender thread can send logs up to the log at the time at which the FLUSH statement is executed to the other server. If used together with the ALL keyword, the current session waits until the most recent log, rather than the log at the time at which the FLUSH statement is executed, is sent to the other server

#### Error Codes

Please refer to the *Error Message Reference*.

#### Example

Assuming that the name of a replication is rep1, replication can be started in one of the following three ways:

-   Replication is started after the data on the local server are transferred to the remote server.

```
iSQL> ALTER REPLICATION rep1 SYNC;
Alter success. 
```

-   Replication is started from the time point at which the replication rep1 was most recently executed.

```
iSQL> ALTER REPLICATION rep1 START;
Alter success.
```

-   Replication is started from the current time point.

```
iSQL> ALTER REPLICATION rep1 QUICKSTART;
Alter success.
```

Use the following commands to check the status of replication after it has started.

(Executing on a local server)

```
iSQL> SELECT rep_name, status, net_error_flag, sender_ip, sender_port,
             peer_ip, peer_port 
      FROM V$REPSENDER;
REP_NAME                                  STATUS               
------------------------------------------------------------------
NET_ERROR_FLAG       
-----------------------
SENDER_IP                                                         SENDER_PORT
---------------------------------------------------------------------------
PEER_IP                                                           PEER_PORT   
---------------------------------------------------------------------------
REP1                                      1                    
0                    
192.168.1.33                                                      11477       
192.168.1.34                                                      21300       
1 row selected.
```

(Executing on a remote server)

```
iSQL> SELECT rep_name, my_ip, my_port, peer_ip, peer_port 
      FROM V$REPRECEIVER;
REP_NAME                                  
--------------------------------------------
MY_IP                                                             MY_PORT     
---------------------------------------------------------------------------
PEER_IP                                                           PEER_PORT   
---------------------------------------------------------------------------
REP1                                      
192.168.1.33                                                      21300       
192.168.1.34                                                      7988        
1 row selected.
```

-   Assuming that the name of a replication is *rep1*, use the following command to stop replication.

```
iSQL> ALTER REPLICATION rep1 STOP;
Alter success.
```

-   • Assuming that the name of a replication is *rep1*, use the following commands to drop a table from a replication object.

```
iSQL> ALTER REPLICATION rep1 STOP;
Alter success.
iSQL> ALTER REPLICATION rep1 DROP TABLE FROM sys.employees TO sys.employees;
Alter success.
```

-   Assuming that the name of a replication is *rep1*, use the following commands to add a table to a replication object.

```
iSQL> ALTER REPLICATION rep1 STOP;
Alter success.
iSQL> ALTER REPLICATION rep1 ADD TABLE FROM sys.employees TO sys.employees;
Alter success.
```

-   If it is desired to check the cumulative time that each Sender replication object has spent waiting for WAIT_NEW_LOG events, execute the following query. This example assumes that the TIMER_THREAD_RESOLUTION property has been set to 1,000,000 microseconds.

```
select rep_name, avg(WAIT_NEW_LOG)/1000000 from x$repsender_statistics where wait_new_log > 0 group by rep_name order by rep_name;
```

-   If it is desired to check the cumulative time that each Receiver replication object has spent waiting for INSERT_ROW events, execute the following query. This example assumes that the TIMER_THREAD_RESOLUTION property has been set to 1,000,000 microseconds

```
select rep_name, avg(INSERT_ROW)/1000000 from x$repreceiver_statistics where recv_xlog > 0 group by rep_name order by rep_name;
```

### DROP REPLICATION 

#### Syntax

```
DROP REPLICATION replication_name;
```

#### Prerequisites

Only the SYS user can execute replication-related statements.

#### Description

This command is used to remove a replication object.

However, once a replication has been dropped, it cannot be executed using ALTER REPLICATION START. Additionally, in order to drop a replication object, it is first necessary to stop it using ALTER REPLICATION STOP.

#### Error Codes

Please refer to the *Error Message Reference*.

#### Example

-   In the following example, a replication object named *rep1* is removed.

```
iSQL> ALTER REPLICATION rep1 STOP;
Alter success.
iSQL> DROP REPLICATION rep1;
Drop success.
```

-   If an attempt is made to remove a replication object without first stopping it, the following error message appears.

```
iSQL> DROP REPLICATION rep1;
[ERR-610FE : Replication has already started.]
```

### Extra Features

Altibase provides the following extra replication features: 

-   Recovery Option
-   Replication Gapless Option
-   Parallel Applier Option
-   Replicated Transaction Grouping Option
-   Meta Logging Option
-   Offline Option

The status of replication option can be confirmed by the value of the OPTIONS column in SYS_REPLICATIONS_meta table. Please refer to the *General Reference* for in-depth information.

#### Recovery Option

##### Syntax

```
CREATE REPLICATION replication_name OPTIONS RECOVERY ...;
ALTER REPLICATION replication_name SET RECOVERY {ENABLE|DISABLE};
```

##### Description

If abnormal server termination occurs during the replication, the user can recover data by using the main transaction which was executed in normally operating server or replicated transaction logs. 

This feature is highly efficient if transaction logs are specified not to be written to disk in COMMIT_WRITE_WAIT_MODE or REPLICATION_COMMIT_WRITE_WAIT_MODE property. For example, a committed transaction can be lost if the system is abnormally shut down. However, in that case, the lost data can be consistent by the replication recovery option.

However, the recovery option cannot be changed while the replication is being processed. In case of not using the recovery option, the recovery related materials the system retains are all released. 

Please refer to the *General Reference* for in-depth information on properties.

##### Restriction

-   The recovery option cannot be used at the same time with the offline option.

##### Example

Assuming that the name of a replication object is rep1, the replication recovery option is used as follows:

-   To enable the replication recovery option:

```
iSQL> ALTER REPLICATION rep1 SET RECOVERY ENABLE;
Alter success.
```

-   To disable the replication recovery option:

```
iSQL> ALTER REPLICATION rep1 SET RECOVERY DISABLE;
Alter success.
```

#### Replication Gapless Option 

##### Syntax

```
CREATE REPLICATION replication_name OPTIONS GAPLESS ...;
ALTER REPLICATION replication_name SET GAPLESS [ENABLE|DISABLE};
```

##### Description

The replication gapless option dissolves replication gaps. If this option is specified and the sender expects the replication gap to still exist after the amount of time set for the REPLICATION_GAPLESS_ALLOW_TIME property, the transaction commit is delayed to buy time for the replication gap to dissolve. The user can set an appropriate value for the REPLICATION_GAPLESS_MAX_WAIT_TIME property to prevent too much time being spent waiting for the replication gap to dissolve before committing the transaction. However, the user should be reminded that delaying transaction commits can degrade service performance. 

For more detailed information about properties, please refer to the General Reference. 

##### Restriction

-   The replication gapless option can only be specified when replication is being performed in LAZY mode.

##### Example 

Assume that there is a replication object named *rep1*. Specify the replication gapless option to dissolve the replication gap for *rep1*. 

-   Specify the replication gapless option.

```
iSQL> CREATE REPLICATION rep1 OPTION GAPLESS;
WITH '192.168.1.12', 35524
FROM sys.employees TO sys.employees,
FROM sys.departments TO sys.departments;;
CREATE success.
```

-   Enable the gapless option.

```
iSQL> ALTER REPLICATION rep1 SET GAPLESS ENABLE;
Alter success.
```

#### Parallel Applier Option

##### Syntax

```
CREATE REPLICATION replication_name OPTIONS PARALLEL receiver_applier_count [buffer_size]...;
ALTER REPLICATION replication_name SET PARALLEL receiver_applier_count [buffer_size];
```

##### Description

The parallel applier creates several appliers that are to apply XLogs to the Storage Manager. The parallel receiver applier option enhances replication performance.

XLogs that the sender sends to the receiver are distributed to the applier in the unit of transactions, so that the XLogs can be applied in parallel. DML statements are executed in parallel and this enhances replication performance. 

Parallel execution requires the synchronization of transaction commits among the parallel appliers to ensure data consistency. During this synchronization process, all threads other than the appliers that are committing transactions wait; the user can anticipate more performance enhancement with a shorter synchronization process. Likewise, the user can anticipate performance degradation if the number of concurrently running transactions is smaller than the number of appliers, because appliers can only execute DML statements under concurrently running transactions, and this would incur unnecessary applier management. 

The parallel receiver applier option is suitable for replications with long-running transactions. Replications with short-running transactions encounter frequent synchronization processes for transaction commits; specifying this option would naturally degrade performance.

receiver_applier_count indicates the number of parallel appliers and can take a value between 0~512. If this value is set to 0, there will be no parallel appliers; in this case, receivers will do the appliers’ job. 

Receivers and appliers use queues to pass XLogs. The REPLICATION_RECEIVER_APPLIER_QUEUE_SIZE property determines the maximum number of XLogs that can be sent. If no value is entered, the value is set according to the following property.

The buffer_size property specifies the initial size of the queue. Values range from 0 to 1 TB. If this value is not specified or if the number of parallel applier queues is less than the property REPLICATION_RECEIVER_APPLIER_QUEUE_SIZE value, the number of parallel applier queues is set to the value specified in the property REPLICATION_RECEIVER_APPLIER_QUEUE_SIZE.

If the unit (K, M, G) is not input, it is recognized in units of Megabytes.

For more detailed information about properties, please refer to the *General Reference*.

##### Example

```
iSQL> CREATE REPLICATION replication_name OPTIONS PARALLEL receiver_applier_count 100M...;
iSQL> ALTER REPLICATION replication_name SET PARALLEL receiver_applier_count 100;
```

##### Restriction

-   The parallel receiver applier option can only be specified when replication is being performed in LAZY mode.

#### Replicated Transaction Grouping Option

##### Syntax

```
CREATE REPLICATION replication_name OPTIONS GROUPING...;
ALTER REPLICATION replication_name SET GROUPING [ENABLE|DISABLE];
```

##### Description

The replication transaction grouping option accumulates multiple transactions into single groups to reduce the number of transactions to be replayed. 

If the replication transaction grouping option has been specified and a replication gap occurs, the Ahead Analyzer which analyzes logs (before the sender does) and creates replication transaction groups, is created. The Ahead Analyzer analyzes as many XLogs as the value set for the REPLICATION_GROUPING_AHEAD_READ_NEXT_LOG_FILE property and starts with the file of the second largest number to the log file being analyzed by the sender. The REPLICATION_GROUPING_TRANSACTION_MAX_COUNT property determines the maximum number of transactions that can be accumulated into single replication transaction groups. 

Replication transactions are accumulated into two types of groups: committed transactions and rolled back transactions. The sender converts groups of committed transactions into a single transaction, whereas the sender does not send the XLogs for rolled-back transactions.

For more detailed information about properties, please refer to the *General Reference*. 

##### Restriction

-   The replication transaction grouping option can only be specified when replication is being performed in LAZY mode.

#### Meta Logging Option

##### Syntax

```sql
CREATE REPLICATION replication_name OPTIONS META_LOGGING ...;
CREATE REPLICATION replication_name FOR ANALYSIS OPTIONS META_LOGGING...;
```

##### Description

The Meta Logging Option is a feature that saves the sender's metadata and restart SN information to a file.

This option is configured on the Active server's replication object. When performing offline replication on the replication server where the receiver thread is running, the saved file can be referenced to retrieve the Active server's metadata.

##### Explanation of the Syntax

###### OPTIONS META_LOGGING

When creating a replication object, the Meta Logging Option is configured.

The sender's metadata and restart SN (Sequence Number) information are saved to the `repl_meta_files` directory in the log file path.

###### FOR ANALYSIS OPTIONS META_LOGGING

When creating a replication object with the Log Analyzer role, the Meta Logging Option is also configured.

The sender's metadata and restart SN information are saved to the `ala_meta_files` directory in the log file path.

> **Reference:**
> For detailed information about the offline option used with the Log Analyzer role replication object in Adapter for JDBC and Adapter for Oracle, please refer to the following document.
>
> - [*Adapter for JDBC User’s Manual - Offline Option*](https://github.com/ALTIBASE/Documents/blob/master/Manuals/Altibase_trunk/eng/Adapter%20for%20JDBC%20User's%20Manual.md#offline-option)
> - [*Adapter for Oracle User’s Manual - Offline Option*](https://github.com/ALTIBASE/Documents/blob/master/Manuals/Altibase_trunk/eng/Adapter%20for%20Oracle%20User's%20Manual.md)

#### Offline Option

##### Syntax

```
CREATE REPLICATION replication_name OPTIONS OFFLINE 'log_dir' ...;

ALTER REPLICATION replication_name SET OFFLINE ENABLE WITH 'log_dir';
ALTER REPLICATION replication_name BUILD OFFLINE META [AT SN(sn)];
ALTER REPLICATION replication_name START WITH OFFLINE;
ALTER REPLICATION replication_name RESET OFFLINE META;
ALTER REPLICATION replication_name SET OFFLINE DISABLE;
```

##### Description

The Offline Option is a feature that retrieves untransmitted logs from the Active server and applies the change transactions to the remote server. This function is set and performed on the replication server where the receiver thread is active, and it is also referred to as offline replication.

If a failure occurs on the Altibase server, preventing the replication of change transactions to the remote server, offline replication can be performed to retrieve the untransmitted logs and apply the changes.

To perform offline replication, the following conditions must be met:

- The Active server must have a history of starting replication to the remote server.
- The Meta Logging Option must be set on the replication object of the Active server.
- The log files of the Active server and the sender's metadata files must be accessible.

##### Explanation of the Syntax

###### OPTIONS OFFLINE

When creating the replication object, set the offline option. In `log_dir`, enter the log file path of the Active server.

###### SET OFFLINE ENABLE WITH

Set the offline option on the existing replication object. This can only be done when replication is stopped. In `log_dir`, enter the log file path of the Active server.

###### BUILD OFFLINE META

Configure the metadata required for offline replication.

When executing this command, it reads the sender's metadata and restart SN files from the `repl_meta_files` directory in the `log_dir` path to configure the metadata. After restarting the Altibase server, the metadata will be lost, so you will need to execute BUILD OFFLINE META again.

###### START WITH OFFLINE  

Perform offline replication. Offline replication is a one-time operation that retrieves the logs not sent by the Active server and applies them, then automatically terminates.

Before performing offline replication, SQL Apply Mode must be enabled, and it should be disabled after the operation is complete.

When offline replication is executed, both the sender and receiver threads are automatically stopped, so replication must be restarted afterward.

###### RESET OFFLINE META

The RESET OFFLINE META command is used to reset the metadata of offline replication after executing BUILD OFFLINE META. It can be performed in the following situations:

- When an error occurs during offline replication and the metadata needs to be reconfigured.
- When offline replication is no longer needed and the metadata is no longer required.

###### SET OFFLINE DISABLE  

Disable the offline option on the replication object. This can only be done when replication is stopped.

<br>Below is a diagram illustrating the process of offline replication.

![](media/Replication/replication-figure-3-1.png)

[Figure 3-1] Data Accordance Between Both Servers

##### Restrictions

- The offline option can only be set on replication objects in LAZY mode.
- The offline option cannot be set on replication objects that include compressed tables.
- The offline option cannot be set simultaneously with the recovery option.
- The server performing offline replication and the Active server must have the same OS, CPU type, and CPU bit architecture. Heterogeneous offline replication is not supported.
- The server performing offline replication and the Active server must have the same three-part binary database version (Major, Minor, Patch).
- The server performing offline replication and the Active server must have the same log file size (LOG_FILE_SIZE).

##### Cautions

If the user arbitrarily changes the log files or sender metadata files, issues such as abnormal termination of the Altibase server may occur.

**Examples of incorrect changes:**

- Renaming files
- Copying log files to another system
- Deleting files

##### Offline Replication Procedure Example

This procedure describes how to perform offline replication on the Standby server when the Active server experiences a failure.

- **Active Server**: The replication server where change transactions occur.
- **Standby Server**: The replication server that performs offline replication.
- **Log file path of the Active server**: `/active_server/altibase_home/logs`

###### Offline Replication on a Replication Object with Offline Option Set

In this example, the Active server has Meta Logging Option set, and the Standby server has the Offline option enabled.

|                            | Active                                                       | Standby                                                      |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1. Schema Creation             | CREATE TABLE t1 (i1 INTEGER PRIMARY KEY, i2 CHAR(20));       | CREATE TABLE t1 (i1 INTEGER PRIMARY KEY, i2 CHAR(20));       |
| 2. Replication Creation             | CREATE REPLICATION rep1 OPTIONS META_LOGGING WITH 'standby_ip', standby_port FROM SYS.t1 to SYS.t1; | CREATE REPLICATION rep1 OPTION OFFLINE '/active_server/altibase_home/logs' WITH 'active_ip', active_port FROM SYS.t1 to SYS.t1; |
| 3. Start Replication on Active Server | ATER REPLICATION START rep1;                                 |                                                              |
| 4. Active Server Failure   | Failure Occurrence                                                    |                                                              |
| 5. Enable SQL Apply Mode    |                                                              | ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;           |
| 6. Configure Offline Metadata |                                                              | ALTER REPLICATION rep1 BUILD OFFLINE META;                   |
| 7. Start Offline Replication    |                                                              | ALTER REPLICATION rep1 START WITH OFFLINE;                   |
| 8. Disable SQL Apply Mode  |                                                              | ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;           |

###### Offline Replication on a Replication Object Without Offline Option Set

This example uses an Active server with the Meta Logging Option enabled and a Standby server without the offline option enabled.

|                            | Active                                                       | Standby                                                      |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1. Schema Creation             | CREATE TABLE t1 (i1 INTEGER PRIMARY KEY, i2 CHAR(20));       | CREATE TABLE t1 (i1 INTEGER PRIMARY KEY, i2 CHAR(20));       |
| 2. Replication Creation             | CREATE REPLICATION rep1 OPTIONS META_LOGGING WITH 'standby_ip', standby_port FROM SYS.t1 to SYS.t1; | CREATE REPLICATION rep1 WITH 'active_ip', active_port FROM SYS.t1 to SYS.t1; |
| 3. Start Replication on Active Server | ATER REPLICATION START rep1;                                 |                                                              |
| 4. Active Server Failure   | Failure Occurrence                                                    |                                                              |
| 5. Enable SQL Apply Mode    |                                                              | ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;           |
| 6. Setting the Offline Option |                                                              | ALTER REPLICATION rep1 SET OFFLINE ENABLE WITH '/active_server/altibase_home/logs'; |
| 7. Configure Offline Metadata |                                                              | ALTER REPLICATION rep1 BUILD OFFLINE META;                   |
| 8. Start Offline Replication    |                                                              | ALTER REPLICATION rep1 START WITH OFFLINE;                   |
| 9. Disabling the Offline Option |                                                              | ALTER REPLICATION rep1 SET OFFLINE DISABLE;                  |
| 10. Disable SQL Apply Mode |                                                              | ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;           |


> **Reference:**
>
> For examples of using the offline option in Adapter for JDBC and Adapter for Oracle, refer to the following document.
>
> - [*Adapter for JDBC User’s Manual - Offline Option*](https://github.com/ALTIBASE/Documents/blob/master/Manuals/Altibase_trunk/eng/Adapter%20for%20JDBC%20User's%20Manual.md#offline-option)
> - [*Adapter for Oracle User’s Manual - Offline Option*](https://github.com/ALTIBASE/Documents/blob/master/Manuals/Altibase_trunk/eng/Adapter%20for%20Oracle%20User's%20Manual.md)

### Replication in a Multiple IP Network Environment

Replication is supported in a multiple IP network environment. In other words, it is possible to perform replication between two hosts having two or more physical network connections.

#### Syntax

```
CREATE REPLICATION replication_name {as master|as slave} 
WITH 'remotehostip', remoteportno 'remotehostip', remoteportno …
FROM user.localtableA TO user.remotetableA,
FROM user.localtableB TO user.remotetableB, …, 
FROM user.localtableC TO user.remotetableC;

ALTER REPLICATION replication_name
ADD HOST ‘remote_host_ip‘, remote_port_no [USING conn_type [ib_latency]];

ALTER REPLICATION replication_name
DROP HOST ‘remotehostip‘, remoteportno;

ALTER REPLICATION replication_name
SET HOST ‘remotehostip‘, remoteportno;
```

#### Description

In order to ensure high system performance and quickly overcome faults, systems can have multiple physical IP addresses assigned to them when a replication object is created. In such an environment, the Sender thread uses the first IP address to access peers and perform replication tasks when replication starts, but if a problem occurs while this task is underway, the Sender thread stops using this connection, connects using another IP address, and tries again.

-   CREATE REPLICATION  
    The name of the replication object is first specified, and then in the WITH clause, the IP addresses and reception ports of multiple remote servers are specified, with commas between each IP address and port, and with spaces between address/port pairs defining each host. The owner and name of the target table(s) on the local server are specified in the FROM clause and the owner and name of the corresponding target table(s) on the remote server are specified in the TO clause, with commas between multiple table specifications.

-   ALTER REPLICATION (ADD HOST):  
    This adds a host. A host can be added to a replication object after the replication object has been stopped. When ADD HOST is executed, before the Sender thread actually adds the host, the connection must be re-established using the IP address that was previously being used

-   *conn_type*  
    This is the communication method with a remote server (TCP/InfiniBand). The default is TCP.

-   *ib_latency*  
    This is the RDMA_LATENCY option value for rsocket. It can only be entered when conn_type is IB.

-   ALTER REPLICATION (DROP HOST) :  
    This drops a host. A host can be dropped from a replication object after the replication object has been stopped. When DROP HOST is executed, the Sender thread attempts to reconnect using the very first IP address.

-   ALTER REPLICATION (SET HOST) :  
    This means setting a particular host as the current host. The current host can be specified after the replication object has been stopped. After execution, the Sender thread attempts to connect using the currently designated IP address.

#### Examples

In the following double-IP network environment, a replication object having a table called employees and one called departments as its target objects is created, and then replication in Active-Standby mode is executed on the local server (IP: 192.168.1.51, PORT NO: 30570) and the remote server (‘IP: 192.168.1.154, PORT NO: 30570’, ‘IP: 192.168.2.154, PORT NO: 30570’).

-   On the remote (standby) server:

```
iSQL> CREATE REPLICATION rep1	
WITH '192.168.1.51', 30570	
FROM sys.employees TO sys.employees,
FROM sys.departments TO sys.departments;
Create success.
```

-   On the local (active) server:

```
iSQL> CREATE REPLICATION rep1
       WITH '192.168.1.154',30570 '192.168.2.154',30570
FROM sys.employees TO sys.employees,
FROM sys.departments TO sys.departments;
Create success.                               
	
iSQL> SELECT * FROM system_.sys_replications_;                               
```

<- The meta table enables the user to view the number of registered hosts, the number of replication target tables, and other related information.

```
REPLICATION_NAME        LAST_USED_HOST_NO    HOST_COUNT  
------------------------------------------------------------------------
IS_STARTED  XSN         ITEM_COUNT  CONFLICT_RESOLUTION REPL_MODE   
------------------------------------------------------------------------
ROLE        OPTIONS     INVALID_RECOVERY REMOTE_FAULT_DETECT_TIME
-----------------------------------------------------------------------
REP1                    2                    2           
0           -1          2           0                   0           
0           0           0                        
1 row selected.

iSQL> SELECT * FROM system_.sys_repl_hosts_;
SYS_REPL_HOSTS_.HOST_NO SYS_REPL_HOSTS_.REPLICATION_NAME          
-----------------------------------------------
SYS_REPL_HOSTS_.HOST_IP                   SYS_REPL_HOSTS_.PORT_NO 
-----------------------------------------------
2           REP1                                      
192.168.1.154                             30570       
3           REP1                                      
192.168.2.154                             30570       
2 rows selected.
```

<- Information about remote server by using meta table.

```
iSQL> ALTER REPLICATION rep1 START;
Alter success.
```

\<- Replication starts.

```
iSQL> SELECT rep_name, status, net_error_flag, sender_ip, sender_port,
             peer_ip, peer_port
FROM V$REPSENDER;
REP_NAME                                  STATUS               
------------------------------------------------------------------
NET_ERROR_FLAG       
-----------------------
SENDER_IP                                                         SENDER_PORT
------------------------------------------------------------------------PEER_IP                                                           PEER_PORT   
------------------------------------------------------------------------REP1                                      1                    
0                    
192.168.1.51                                                      13718       
192.168.1.154                                                     30570       
1 row selected. 
```

<- The status of replication is checked after replication starts. The Sender thread connects to the peer using the first IP and PORT.

!!!!!!!!!!!!! Network line disconnection !!!!!!!!!!!!!!!

```
<- The status of replication is checked after replication starts. The Sender thread connects to the peer using the first IP and PORT.iSQL> SELECT rep_name, status, net_error_flag, sender_ip, sender_port,
             peer_ip, peer_port 
FROM V$REPSENDER;
REP_NAME                                  STATUS               
------------------------------------------------------------------
NET_ERROR_FLAG       
-----------------------
SENDER_IP                                                         SENDER_PORT
-----------------------------------------------------------------------
PEER_IP                                                           PEER_PORT   
-----------------------------------------------------------------------
REP1                                      1                    
0                    
192.168.1.51                                                      40009       
192.168.1.154                                                     30570       
1 row selected. 
```

\<- The status of replication is checked after network failure occurs. This verifies reconnection using the second IP and PORT.

```
iSQL> ALTER REPLICATION rep1 STOP;
Alter success.
```

\<- Replication is stopped.

```
iSQL> ALTER REPLICATION rep1 START;
Alter success.
```

\<- Replication starts.

```
iSQL> SELECT rep_name, status, net_error_flag, sender_ip, sender_port,
             peer_ip, peer_port 
FROM V$REPSENDER;
REP_NAME                                  STATUS               
------------------------------------------------------------------
NET_ERROR_FLAG       
-----------------------
SENDER_IP                                                         SENDER_PORT
-----------------------------------------------------------------------
PEER_IP                                                           PEER_PORT   
-----------------------------------------------------------------------
REP1                                      1                    
0                    
192.168.1.51                                                      64351       
192.168.1.154                                                     30570       
1 row selected.
```

\<- When replication is started again after having been stopped, it can be verified to have been reconnected to the same IP and PORT to which it was connected before being stopped.

```
iSQL> ALTER REPLICATION rep1 ADD HOST '192.168.3.154',30570;
Alter success.
```

\<- Add host: Can be executed after replication.

```
iSQL> ALTER REPLICATION rep1 DROP HOST '192.168.3.154',30570;
Alter success.
```

\<- remove host: Can be executed after replication.

```
iSQL> ALTER REPLICATION rep1 SET HOST '192.168.1.154',30570;
Alter success.
```

\<- Designate the host: Can be executed after replication.

```
iSQL> ALTER REPLICATION rep1 START;
Alter success.
```

\<- Replication is restarted after setting the new host. The replication operation first attempts to connect using the currently designated IP and PORT.

```
iSQL> SELECT rep_name, status, net_error_flag, sender_ip, sender_port, 
             peer_ip, peer_port 
FROM V$REPSENDER;
REP_NAME                                  STATUS               
------------------------------------------------------------------
NET_ERROR_FLAG       
-----------------------
SENDER_IP                                                         SENDER_PORT
-----------------------------------------------------------------------
PEER_IP                                                           PEER_PORT   -----------------------------------------------------------------------
REP1                                      1                    
0                    
192.168.1.51                                                      11477       
192.168.1.154                                                     30570       
1 row selected.
```

<- Connection to the peer using the newly designated IP 192.168.1.154 and PORT number 30570 can be confirmed.

### Replication Related Properties

To use replication, the Altibase properties file should be modified to suit the purposes of the user. The following properties are described in the *General Reference Manual*.

-   REPLICATION_ACK_XLOG_COUNT
-   REPLICATION_ALLOW_DUPLICATE_HOSTS
-   REPLICATION_BEFORE_IMAGE_LOG_ENABLE
-   REPLICATION_COMMIT_WRITE_WAIT_MODE
-   REPLICATION_CONNECT_RECEIVE_TIMEOUT
-   REPLICATION_CONNECT_TIMEOUT
-   REPLICATION_DDL_ENABLE
-   REPLICATION_DDL_ENABLE_LEVEL
-   REPLICATION_DDL_SYNC
-   REPLICATION_DDL_SYNC_TIMEOUT
-   REPLICATION_EAGER_PARALLEL_FACTOR
-   REPLICATION_EAGER_RECEIVER_MAX_ERROR_COUNT
-   REPLICATION_FAILBACK_INCREMENTAL_SYNC
-   REPLICATION_GAP_UNIT
-   REPLICATION_GAPLESS_ALLOW_TIME
-   REPLICATION_GAPLESS_MAX_WAIT_TIME
-   REPLICATION_GROUPING_TRANSACTION_MAX_COUNT
-   REPLICATION_GROUPING_AHEAD_READ_NEXT_LOG_FILE
-   REPLICATION_HBT_DETECT_HIGHWATER_MARK
-   REPLICATION_HBT_DETECT_TIME
-   REPLICATION_IB_LATENCY
-   REPLICATION_IB_PORT_NO
-   REPLICATION_INSERT_REPLACE
-   REPLICATION_KEEP_ALIVE_CNT
-   REPLICATION_LOCK_TIMEOUT
-   REPLICATION_LOG_BUFFER_SIZE
-   REPLICATION_MAX_COUNT
-   REPLICATION_MAX_LISTEN
-   REPLICATION_MAX_LOGFILE
-   REPLICATION_POOL_ELEMENT_COUNT
-   REPLICATION_POOL_ELEMENT_SIZE
-   REPLICATION_PORT_NO
-   REPLICATION_PREFETCH_LOGFILE_COUNT
-   REPLICATION_RECEIVE_TIMEOUT
-   REPLICATION_RECEIVER_APPLIER_ASSIGN_MODE
-   REPLICATION_RECEIVER_APPLIER_QUEUE_SIZE
-   REPLICATION_RECOVERY_MAX_LOGFILE
-   REPLICATION_RECOVERY_MAX_TIME
-   REPLICATION_SENDER_AUTO_START
-   REPLICATION_SENDER_COMPRESS_XLOG
-   REPLICATION_SENDER_ENCRYPT_XLOG
-   REPLICATION_SENDER_SEND_TIMEOUT
-   REPLICATION_SENDER_SLEEP_TIME
-   REPLICATION_SENDER_SLEEP_TIMEOUT
-   REPLICATION_SENDER_START_AFTER_GIVING_UP
-   REPLICATION_SERVER_FAILBACK_MAX_TIME
-   REPLICATION_SQL_APPLY_ENABLE
-   REPLICATION_SYNC_APPLY_METHOD
-   REPLICATION_SYNC_LOCK_TIMEOUT
-   REPLICATION_SYNC_LOG
-   REPLICATION_SYNC_TUPLE_COUNT
-   REPLICATION_TIMESTAMP_RESOLUTION
-   REPLICATION_TRANSACTION_POOL_SIZE
-   REPLICATION_UPDATE_REPLACE

# 4. Executing DDL Statements in a Replication Environment

## Overview

Altibase synchronizes data by transferring transaction logs generated on the local server to the remote server using a network-based replication mechanism. However, transaction logs generated by DDL operations are not transmitted. This is because DDL statements modify metadata on replication targets, which can lead to data inconsistency between servers.

Therefore, in a typical replication environment, to execute a DDL statement, the target object must first be excluded from replication. Then, the DDL operation must be executed independently on each replication node. For more details on standard DDL execution procedures, refer to [Appendix B: Standard DDL Execution Procedure](#appendix-b-standard-ddl-execution-procedure).

This chapter introduces a method for executing DDL statements safely and efficiently in an Altibase replication environment—without removing the replication target.

### **Properties for Executing DDL Statements**

By default, DDL statements cannot be executed on replication targets, with a few exceptions. Therefore, to run DDL statements, the relevant settings must be enabled.

The following are the key properties that must be configured to allow DDL execution on replication targets.

| Property                     | Description                                                  | Default |
| :--------------------------- | :----------------------------------------------------------- | :-----: |
| REPLICATION_DDL_ENABLE       | Enables the execution of DDL statements. When set to `1`, DDL can be executed on replication targets. |    0    |
| REPLICATION_DDL_ENABLE_LEVEL | Specifies the types of DDL statements allowed on replication targets. |    0    |
| REPLICATION_SQL_APPLY_ENABLE | Enables [SQL apply mode](#appendix-c-sql-apply-mode).        |    0    |

### Restrictions

Even when the relevant settings are enabled, DDL statements cannot be executed on replication targets that belong to the following types of replication objects:

- Replication objects with [recovery options](#recovery-option) enabled

  In this case, delete the replication object first, perform the DDL operation, and then recreate the replication object.

- Replication objects operating in EAGER mode

  For such cases, refer to [Appendix B: Standard DDL Execution Procedure](#appendix-b-standard-ddl-execution-procedure).

### **Cautions**

- Executing a DDL statement locks the target table. If a primary transaction occurs during this time, the receiver thread cannot apply the replicated transaction to the locked table.
- You must **clear any replication gap** before executing a DDL statement. Running a DDL with an active replication gap can negatively affect replication performance.
- If the **column range** is being **increased**, execute the DDL first on the server **not generating primary transactions**.
- If the **column range** is being **decreased**, execute the DDL first on the server **generating primary transactions**.

## Allowed DDL Statements

이중화 대상에 수행할 수 있는 DDL 문은 `REPLICATION_DDL_ENABLE_LEVEL` 프로퍼티의 설정 값에 따라 달라지며, 이 값은 0 또는 1로 설정할 수 있다. 

사용자는 수행하려는 DDL 문에 적합하게 이 프로퍼티를 설정해야 한다.

### DDL Level 1

The following DDL statements can be executed when `REPLICATION_DDL_ENABLE_LEVEL` is set to `1`.

> [!IMPORTANT]
>
> To execute statements under DDL Level 1, **[SQL apply mode](#appendix-c-sql-apply-mode) must be enabled**.
>  SQL apply mode is performed on the replication receiver side.

> [!tip]
>
> When `REPLICATION_DDL_ENABLE_LEVEL` is set to `1`, all statements under [DDL Level 0](#ddl-level-0) can also be executed.

#### Adding and Modifying Columns

You can add columns with `NOT NULL` and unique key constraints, or modify the constraints and data types of existing columns.

```sql
ALTER TABLE table_name ADD COLUMN ( column_name DATA_TYPE NOT NULL );
ALTER TABLE table_name ADD COLUMN ( column_name DATA_TYPE UNIQUE );
ALTER TABLE table_name ADD COLUMN ( column_name DATA_TYPE LOCALUNIQUE );

ALTER TABLE table_name ALTER COLUMN ( column_name NOT NULL );
ALTER TABLE table_name ALTER COLUMN ( column_name NULL );

ALTER TABLE table_name MODIFY COLUMN ( column_name NOT NULL );
ALTER TABLE table_name MODIFY COLUMN ( column_name NULL );
ALTER TABLE table_name MODIFY COLUMN ( column_name DATA_TYPE );
```

#### Deleting Columns

You can delete columns that have constraints or are used in function-based indexes.

```sql
ALTER TABLE table_name DROP COLUMN column_name;
```

The following types of columns cannot be deleted:

- Primary key
- Compressed columns

#### Partition Operations

You can split, merge, or drop partitions. Partitions created or removed through partition operations are automatically added to or removed from the replication target partitions.

```sql
ALTER TABLE table_name SPLIT PARTITION .....;
ALTER TABLE table_name MERGE PARTITIONS .....;
ALTER TABLE table_name DROP PARTITION partiton_name;
```

When performing partition operations, take the following precautions:

- Replication must be stopped on **both the local and remote servers**.
- The partition names used in the DDL statement must be identical on both the local and remote servers.
- Partition merging can only be performed when all target partitions are part of the replication target.
- Partition deletion is allowed only if the partitioned table contains at least two partitions.

#### Adding, Modifying, and Dropping Table Constraints

You can add, modify, or drop table constraints.

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name UNIQUE ( column_name );
ALTER TABLE table_name ADD CONSTRAINT constraint_name LOCALUNIQUE ( column_name ) ;
ALTER TABLE table_name ADD CONSTRAINT constraint_name CHECK ( check_condition );
ALTER TABLE table_name RENAME CONSTRAINT constraint_name TO constraint_name;
ALTER TABLE table_name DROP CONSTRAINT constraint_name;
```

#### Creating and Dropping Unique Key Indexes and Function-Based Indexes

You can create or drop unique key indexes and function-based indexes.

```sql
CREATE UNIQUE INDEX index_name ON table_name ( column_name );
CREATE INDEX index_name ON table_name ( expression );
DROP INDEX index_name; 
```

### DDL Level 0

The following DDL statements can be executed when REPLICATION_DDL_ENABLE_LEVEL is set to 0 — that is, under DDL Level 0. 

#### Adding Columns Without Constraints

```sql
ALTER TABLE table_name ADD COLUMN ( column_name DATA_TYPE );
```

The following types of columns **cannot** be added:

- Compressed columns
- Foreign keys
- Columns with [constraints](https://github.com/ALTIBASE/Documents/blob/master/Manuals/Altibase_trunk/eng/Administrator%E2%80%99s%20Manual.md#constraints-2)

#### Deleting Columns Without Constraints

```sql
ALTER TABLE table_name DROP COLUMN column_name;
```

The following types of columns **cannot** be deleted:

- Compressed columns
- Primary keys
- Columns with [constraints](https://github.com/ALTIBASE/Documents/blob/master/Manuals/Altibase_trunk/eng/Administrator%E2%80%99s%20Manual.md#constraints-2)
- Columns used in function-based indexes

#### Setting and Removing Default Values for Columns

```sql
ALTER TABLE table_name ALTER COLUMN ( column_name SET DEFAULT value ); 
ALTER TABLE table_name ALTER COLUMN ( column_name DROP DEFAULT);
```

#### Changing the Tablespace of a Table or Partition

```sql
ALTER TABLE table_name ALTER TABLESPACE tablespace_name;
ALTER TABLE table_name ALTER PARTITION partition_name TABLESPACE;
```

#### Deleting All Data from a Table or Partition

```sql
ALTER TABLE table_name TRUNCATE PARTITION partition_name;
TRUNCATE TABLE table_name;
```

However, data cannot be deleted from tables that contain the following type of column:

- Compressed columns

#### Creating and Dropping Indexes

```sql
CREATE INDEX index_name ON table_name ( column_name );
DROP INDEX index_name;
```

The following types of indexes cannot be dropped:

- Unique key indexes
- Function-based indexes

### Other Statements

The following statement can be executed on replication targets regardless of the `REPLICATION_DDL_ENABLE` property setting:

#### Disk Index AGING

```sql
ALTER INDEX index_name AGING;
```

#### Returning an Empty Page

```sql
ALTER TABLE table_name COMPACT;
ALTER TABLE table_name COMPACT PARTITION partition_name;
```

#### Rebuilding Index Partitions

```sql
ALTER INDEX REBUILD PARTITION index_partition_name;
```

#### Granting and Revoking Privileges

```sql
GRANT OBJECT ...;
REVOKE OBJECT ...;
```

#### Creating and Dropping Triggers

```sql
CREATE TRIGGER ...;
DROP TRIGGER ...;
```

## Executing DDL Statements

This section describes the procedure for executing DDL statements that fall under DDL Level 1 and DDL Level 2 on replication targets. **If the steps are not followed in the recommended order, data inconsistency may occur.**

#### Step 1. Service Migration

1. Migrate all services to the local server where the DDL statement will be executed.

2. Confirm that all services have been successfully migrated to the local server.

   On the remote server, execute the following query and ensure that the result is 0.

   ```sql
   SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();
   ```

#### Step 2. Configure Properties

On both the local and remote servers, update the property settings according to the DDL statement you intend to execute.

```sql
ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;
ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;
ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;
```

#### Step 3. Set the Session Replication Mode

Set the session's replication mode[^3] to `DEFAULT` on both the local and remote servers so that it follows the configuration of the replication object.

```sql
ALTER SESSION SET REPLICATION = DEFAULT;
```

[^3]: When the session replication mode is set to DEFAULT, replication is performed according to the mode defined in the replication object (either LAZY or EAGER).

#### Step 4. Execute the DDL Statement

Execute the same DDL statement on both the local and remote servers.

##### 1) Resolve any remaining replication gaps before executing the DDL statement.

```sql
ALTER REPLICATION replication_name FLUSH;
```

##### 2) Stop replication before executing the DDL (for partitioned targets).

```sql
ALTER REPLICATON replication_name STOP;
```

##### 3) Execute the DDL statement.

##### 4) Restart replication after executing the DDL (for partitioned targets).

``` sql
ALTER REPLICATON replication_name START;
```

##### 5) Resolve the replication gap after executing the DDL (if SQL apply mode is enabled).

```sql
ALTER REPLICATION replication_name FLUSH;
```

#### Step 5. Verify SQL Apply Mode Operation

On the remote server, check whether SQL apply mode is active for any replication object.

If the DDL statements have been executed correctly on the replication target server, there should be no replication objects currently operating in SQL apply mode.

Execute the following query to confirm that the SQL_APPLY_TABLE_COUNT value is 0.

```sql
SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;
```

This procedure is performed only when SQL apply mode is enabled.

#### Step 6. Restore Property Settings

Immediately after completing the DDL operation, revert the values of the properties modified in Step 2 back to their default settings.

```sql
ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;
ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;
ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;
```

#### Step 7. Service Distribution

Distribute the services back to their original configuration.

#### Operation Procedure Table

<table border="1" cellpadding="5" cellspacing="0">   
    <thead>     
        <tr>       
            <th colspan="2">Step</th>       
            <th>DDL Level 0</th>       
            <th>DDL Level 1 : Table or Column Targets</th>       
            <th>DDL Level 1 : Partition Targets</th>     
        </tr>   
    </thead>   
    <tbody>     
        <tr>       
            <td rowspan="2">Step 1. Service Migration</td>       
            <td>Service Migration</td>       
            <td>Migrate the service to the local server where the DDL statement will be executed.</td>       
            <td>Migrate the service to the local server where the DDL statement will be executed.</td>       
            <td>Migrate the service to the local server where the DDL statement will be executed.</td>     
        </tr>     
        <tr>       
            <td>Verify the service migration</td>       
            <td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>       
            <td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>       
            <td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>     
        </tr>     
        <tr>       
            <td rowspan="3">Step 2. Configure Properties</td>       
            <td>Enable DDL Statement Execution</td>       
            <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>       
            <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>       
            <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>     
        </tr>     
        <tr>       
            <td>Set DDL Execution Level</td>       
            <td>-</td>       
            <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>       
            <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>     
        </tr>     
        <tr>       
            <td>Enable SQL Apply Mode</td>       
            <td>-</td>       
            <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>       
            <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>     
        </tr>     
        <tr>       
            <td colspan="2">Step 3. Set Session Replication Mode</td>            
            <td>ALTER SESSION SET REPLICATION_MODE = DEFAULT;</td>       
            <td>ALTER SESSION SET REPLICATION_MODE = DEFAULT;</td>       
            <td>ALTER SESSION SET REPLICATION_MODE = DEFAULT;</td>     
        </tr>     
        <tr>       
            <td rowspan="5">Step 4. Execute the DDL Statement</td>       
            <td>Resolve Replication Gap</td>       
            <td>ALTER REPLICATION replication_name FLUSH;</td>       
            <td>ALTER REPLICATION replication_name FLUSH;</td>       
            <td>ALTER REPLICATION replication_name FLUSH;</td>     
        </tr>     
        <tr>       
            <td>Stop Replication (Partition Targets)</td>       
            <td>-</td>       
            <td>-</td>       
            <td>ALTER REPLICATON replication_name STOP;</td>     
        </tr>     
        <tr>       
            <td>Execute the DDL Statement</td>       
            <td>Execute the DDL Statement</td>       
            <td>Execute the DDL Statement</td>       
            <td>Execute the DDL Statement</td>     
        </tr>     
        <tr>       
            <td>Start Replication (Partition Targets)</td>       
            <td>-</td>       
            <td>-</td>       
            <td>ALTER REPLICATON replication_name START;</td>     
        </tr>     
        <tr>       
            <td>Resolve Replication Gap (When SQL Apply Mode Is Enabled)</td>       
            <td>-</td>       
            <td>ALTER REPLICATION replication_name FLUSH;</td>       
            <td>ALTER REPLICATION replication_name FLUSH;</td>     
        </tr>     
        <tr>       
            <td colspan="2">Step 5. Verify SQL Apply Mode Operation</td>        
            <td>-</td>       
            <td>SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;</td>       
            <td>SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;</td>     
        </tr>     
        <tr>       
            <td rowspan="3">Step 6. Restore Property Settings</td>       
            <td>Disable DDL Statement Execution</td>       
            <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>       
            <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>       
            <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>     
        </tr>     
        <tr>       
            <td>Set DDL Execution Level</td>       
            <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>       
            <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>       
            <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>     
        </tr>     
        <tr>       
            <td>Disable SQL Apply Mode</td>       
            <td>-</td>       
            <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>       
            <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>     
        </tr>     
        <tr>       
            <td  colspan="2" rowspan="2">Step 7. Service Distribution</td>           
            <td>Redistribute the Service to Its Original Configuration.</td>       
            <td>Redistribute the Service to Its Original Configuration.</td>       
            <td>Redistribute the Service to Its Original Configuration.</td>     
        </tr>   
    </tbody> 
</table>




## DDL Execution Example

### DDL Level 1 Example

#### Example 1: Changing the Data Type of a Column — CHAR(5) to CHAR(10)

The following example demonstrates how to change the data type of column `c2` in replication target table `T1`, which belongs to the replication object `rep1`, from `CHAR(5)` to `CHAR(10)`.

This case covers changes to a **wider data type** than the original.

> [!IMPORTANT]
>
> **When changing to a wider data type,** the DDL statement must be executed first on the server where no primary transactions are occurring.

##### Active-Standby environment 

<table border="1" cellpadding="5" cellspacing="0">
  <thead>
    <tr>      
      <th colspan="2">Step</th>
      <th>Active</th>
      <th>Standby</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="2">Step 1. Service Migration</td>
      <td>There are no services to migrate since this is an Active-Standby environment.</td>
      <td></td>
    </tr>
    <tr>
      <td rowspan="3">Step 2. Configure Properties</td>
      <td>Enable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
    </tr>
    <tr>
      <td>Enable SQL Apply Mode</td>
      <td></td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
    </tr>
    <tr>    
      <td colspan="2">Step 3. Set Session Replication Mode</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
      <td></td>
    </tr>
    <tr>           
      <td rowspan="4">Step 4. Execute the DDL Statement</td>
      <td>Execute the DDL Statement</td>
      <td></td>
      <td>ALTER TABLE T1 MODIFY COLUMN ( c2 CHAR(10) );</td>
    </tr>     
    <tr>
      <td>Resolve Replication Gap Before Executing the DDL Statement</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>       
    <tr>
      <td>Execute the DDL Statement</td>
      <td>ALTER TABLE T1 MODIFY COLUMN ( c2 CHAR(10) );</td>
      <td></td>
    </tr>
    <tr>
      <td>Resolve Replication Gap After Executing the DDL Statement(When SQL Apply Mode is Enabled)</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>      
    <tr>       
      <td colspan="2">Step 5. Verify SQL Apply Mode Operation</td>
      <td></td>
      <td>SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;</td>
    </tr>
    <tr>                  
      <td rowspan="3">Step 6. Restore Property Settings</td>
      <td>Disable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
    </tr>
    <tr>
      <td>Disable SQL Apply Mode</td>
      <td></td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
    </tr>
    <tr>                  
      <td colspan="2">Step 7. Service Distribution</td>
      <td>There are no services to migrate since this is an Active-Standby environment.</td>
      <td></td>
    </tr>
  </tbody>
</table>



##### Active-Active environment 

Assume that Active1 is the local server where the DDL statement is executed and primary transactions are occurring.

<table border="1" cellpadding="5" cellspacing="0">
  <thead>
    <tr>
      <th colspan="2">Step</th>
      <th>Active1</th>
      <th>Active2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Step 1. Service Migration</td>
      <td>Service Migration</td>
      <td></td>
      <td>Migrate the service to Active1.</td>
    </tr>
    <tr>
      <td>Verify the service migration</td>
      <td></td>
      <td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
    </tr>
    <tr>
      <td rowspan="3">Step 2. Configure Properties</td>
      <td>Enable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
    </tr>
    <tr>
      <td>Enable SQL Apply Mode</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
    </tr>
    <tr>
      <td colspan="2">Step 3. Set Session Replication Mode</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
    </tr>
    <tr>
      <td rowspan="6">Step 4. Execute the DDL Statement</td>
      <td>Resolve Replication Gap Before Executing the DDL Statement</td>
      <td></td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td></td>
      <td>ALTER TABLE t1 MODIFY COLUMN ( C2 CHAR(10) );</td>
    </tr>
    <tr>
      <td>Resolve Replication Gap After Executing the DDL Statement(When SQL Apply Mode is Enabled)</td>
      <td></td>        
      <td>ALTER REPLICATION rep1 FLUSH;</td>
    </tr>
    <tr>
      <td>Resolve Replication Gap Before Executing the DDL Statement</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td>ALTER TABLE t1 MODIFY COLUMN ( C2 CHAR(10) );</td>
      <td></td>
    </tr>
    <tr>
      <td>Resolve Replication Gap After Executing the DDL Statement(When SQL Apply Mode is Enabled)</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>      
    <tr>
      <td colspan="2">Step 5. Verify SQL Apply Mode Operation</td>
      <td>SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;</td>
      <td>SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;</td>
    </tr>
    <tr>
      <td rowspan="3">Step 6. Restore Property Settings</td>
      <td>Disable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
    </tr>
    <tr>
      <td>Disable SQL Apply Mode</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
    </tr>
    <tr>
      <td colspan="2">Step 7. Service Distribution</td>
      <td>Distribute the service to Active2.</td>
      <td></td>
    </tr>
  </tbody>
</table>




#### Example 2: Adding a Table Constraint – CHECK

The following example demonstrates how to add a `CHECK` constraint to column *`c2`* of the replication target table *`T1`*, which belongs to the replication object *`rep1`*.

This case deals with restricting the allowed value range of a column more narrowly than before.

> [!IMPORTANT]
>
> **When narrowing the value range of a column**, the DDL statement must be executed first on the server where primary transactions are occurring.

##### Active-Standby Environment

<table border="1" cellpadding="5" cellspacing="0">
  <thead>
    <tr>
      <th colspan="2">Step</th>
      <th>Active</th>
      <th>Standby</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="2">Step 1. Service Migration</td>
      <td>There are no services to migrate since this is an Active-Standby environment.</td>
      <td></td>
    </tr>
    <tr>
      <td rowspan="3">Step 2. Configure Properties</td>
      <td>Enable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
    </tr>
    <tr>
      <td>Enable SQL Apply Mode</td>
      <td></td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
    </tr>
    <tr>
      <td colspan="2">Step 3. Set Session Replication Mode</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
      <td></td>
    </tr>
    <tr>
      <td rowspan="4">Step 4. Execute the DDL Statement</td>
      <td>Resolve Replication Gap</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td>ALTER TABLE T1 ADD CONSTRAINT T1_CHECK CHECK ( c2 &lt; 10 );</td>
      <td></td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td></td>
      <td>ALTER TABLE T1 ADD CONSTRAINT T1_CHECK CHECK ( c2 &lt; 10 );</td>
    </tr>
    <tr>
      <td>Resolve Replication Gap(When SQL Apply Mode Is Enabled)</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>
    <tr>
      <td colspan="2">Step 5. Verify SQL Apply Mode Operation</td>
      <td></td>
      <td>SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;</td>
    </tr>
    <tr>
      <td rowspan="3">Step 6. Restore Property Settings</td>
      <td>Disable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
    </tr>
    <tr>
      <td>Disable SQL Apply Mode</td>
      <td></td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
    </tr>
    <tr>
      <td colspan="2">Step 7. Service Distribution</td>
      <td>There are no services to migrate since this is an Active-Standby environment.</td>
      <td></td>
    </tr>
  </tbody>
</table>






##### Active-Active Environment

Assume that Active1 is the local server where DDL statements are executed and primary transactions are occurring.

<table border="1" cellpadding="5" cellspacing="0">
  <thead>
    <tr>
      <th colspan="2">Step</th>
      <th>Active1</th>
      <th>Active2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Step 1. Service Migration</td>
      <td>Service Migration</td>
      <td></td>
      <td>Migrate the service to Active1.</td>
    </tr>
    <tr>
      <td>Verify the service migration</td>
      <td></td>
      <td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
    </tr>
    <tr>
      <td rowspan="3">Step 2. Configure Properties</td>
      <td>Enable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
    </tr>
    <tr>
      <td>Enable SQL Apply Mode</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
    </tr>
    <tr>
      <td colspan="2">Step 3. Set Session Replication Mode</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
    </tr>
    <tr>
      <td rowspan="6">Step. 4. Execute the DDL Statement</td>
      <td>Resolve Replication Gap Before Executing the DDL Statement</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td>ALTER TABLE t1 ADD CONSTRAINT T1_CHECK CHECK ( C2 &lt; 10 );</td>
      <td></td>
    </tr>
    <tr>
      <td>Resolve Replication Gap After Executing the DDL Statement(When SQL Apply Mode Is Enabled)</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>      
    <tr>
      <td>Resolve Replication Gap Before Executing the DDL Statement</td>
      <td></td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td></td>
      <td>ALTER TABLE t1 ADD CONSTRAINT T1_CHECK CHECK ( C2 &lt; 10 );</td>
    </tr>
    <tr>
      <td>Resolve Replication Gap After Executing the DDL Statement(When SQL Apply Mode Is Enabled)</td>
      <td></td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
    </tr>      
    <tr>
      <td colspan="2">Step 5. Verify SQL Apply Mode Operation</td>
      <td>SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;</td>
      <td>SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;</td>
    </tr>
    <tr>
      <td rowspan="3">Step 6. Restore Property Settings</td>
      <td>Disable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
    </tr>
    <tr>
      <td>Disable SQL Apply Mode</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
    </tr>
    <tr>
      <td colspan="2">Step 7. Service Distribution</td>
      <td>Distribute the service to Active2.</td>
      <td></td>
    </tr>
  </tbody>
</table>




#### Example 3: Partition Split

The following example demonstrates how to split partition *`P2`* of the replication target table *`T1`*, which belongs to the replication object *`rep1`*, into two partitions: *`P3`* and *`P4`*.

##### Active-Standby Environment

<table border="1" cellpadding="5" cellspacing="0">
  <thead>
    <tr>
      <th colspan="2">Step</th>
      <th>Active</th>
      <th>Standby</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="2">Step 1. Service Migration</td>
      <td>There are no services to migrate since this is an Active-Standby environment.</td>
      <td></td>
    </tr>
    <tr>
      <td rowspan="3">Step 2. Configure Properties</td>
      <td>Enable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
    </tr>
    <tr>
      <td>Enable SQL Apply Mode</td>
      <td></td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
    </tr>
    <tr>
      <td colspan="2">Step 3. Set Session Replication Mode</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
      <td></td>
    </tr>
    <tr>
      <td rowspan="5">Step 4. Execute the DDL Statement</td>
      <td>Resolve Replication Gap</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>
    <tr>
      <td>Stop Replication</td>
      <td>ALTER REPLICATION rep1 STOP;</td>
      <td></td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td>ALTER TABLE T1 SPLIT PARTITION P2 INTO (PARTITION P3, PARTITION P4);</td>
      <td>ALTER TABLE T1 SPLIT PARTITION P2 INTO (PARTITION P3, PARTITION P4);</td>
    </tr>
    <tr>
      <td>Start Replication</td>
      <td>ALTER REPLICATION rep1 START;</td>
      <td></td>
    </tr>
    <tr>      
      <td>Resolve Replication Gap(When SQL Apply Mode Is Enabled)</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>       
    <tr>
      <td colspan="2">Step 5. Verify SQL Apply Mode Operation</td>
      <td></td>
      <td>SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;</td>
    </tr>
    <tr>
      <td rowspan="3">Step 6. Restore Property Settings</td>
      <td>Disable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
    </tr>
    <tr>
      <td>Disable SQL Apply Mode</td>
      <td></td>
      <td>REPLICATION_SQL_APPLY_ENABLE = 0;</td>
    </tr>
    <tr>
      <td colspan="2">Step 7. Service Distribution</td>
      <td>There are no services to migrate since this is an Active-Standby environment.</td>
      <td></td>
    </tr>
  </tbody>
</table>







##### Active-Active Environment

Assume that Active1 is the local server where DDL statements are executed and primary transactions are occurring.

<table border="1" cellpadding="5" cellspacing="0">
  <thead>
    <tr>
      <th colspan="2">Step</th>
      <th>Active1</th>
      <th>Active2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Step 1. Service Migration</td>
      <td>Service Migration</td>
      <td></td>
      <td>Migrate the service to Active1.</td>
    </tr>
    <tr>
      <td>Verify the service migration</td>
      <td></td>
      <td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
    </tr>
    <tr>
      <td rowspan="3">Step 2. Configure Properties</td>
      <td>Enable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
    </tr>
    <tr>
      <td>Enable SQL Apply Mode</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
    </tr>
    <tr>
      <td colspan="2">Step 3. Set Session Replication Mode</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
    </tr>
    <tr>
      <td rowspan="5">Step 4. Execute the DDL Statement</td>
      <td>Resolve Replication Gap</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
    </tr>
    <tr>
      <td>Stop Replication</td>
      <td>ALTER REPLICATION rep1 STOP;</td>
      <td>ALTER REPLICATION rep1 STOP;</td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td>ALTER TABLE T1 SPLIT PARTITION P2 INTO (PARTITION P3, PARTITION P4);</td>
      <td>ALTER TABLE T1 SPLIT PARTITION P2 INTO (PARTITION P3, PARTITION P4);</td>
    </tr>
    <tr>
      <td>Start Replication</td>
      <td>ALTER REPLICATION rep1 START;</td>
      <td>ALTER REPLICATION rep1 START;</td>
    </tr>
    <tr>
      <td>Resolve Replication Gap(When SQL Apply Mode Is Enabled)</td>
      <td>ALTER REPLICATION rep1 FLUSH</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
    </tr>    
    <tr>
      <td colspan="2">Step 5. Verify SQL Apply Mode Operation</td>
      <td>SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;</td>
      <td>SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;</td>
    </tr>
    <tr>
      <td rowspan="3">Step 6. Restore Property Settings</td>
      <td>Disable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
    </tr>
    <tr>
      <td>Disable SQL Apply Mode</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
    </tr>
    <tr>
      <td colspan="2">Step 7. Service Distribution</td>
      <td>Distribute the service to Active2.</td>
      <td></td>
    </tr>
  </tbody>
</table>







### DDL Level 0 Example

#### Example 1: Adding a Column

The following example demonstrates how to add column *`i3`* to the replication target table *`T1`*, which belongs to the replication object *`rep1`*.

##### Active-Standby Environment

<table border="1" cellpadding="5" cellspacing="0">
  <thead>
    <tr>
      <th colspan="2">Step</th>
      <th>Active</th>
      <th>Standby</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="2">Step 1. Service Migration</td>
      <td>There are no services to migrate since this is an Active-Standby environment.</td>
      <td></td>
    </tr>
    <tr>
      <td>Step 2. Configure Properties</td>
      <td>Enable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
    </tr>
    <tr>
      <td colspan="2">Step 3. Set Session Replication Mode</td>  
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
      <td></td>
    </tr>
    <tr>
      <td rowspan="4">Step 4. Execute the DDL Statement</td>
      <td>Execute the DDL Statement</td>
      <td></td>
      <td>ALTER TABLE T1 ADD COLUMN ( i3 INTEGER );</td>
    </tr>
    <tr>
      <td>Resolve Replication Gap</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td>ALTER TABLE T1 ADD COLUMN ( i3 INTEGER );</td>
      <td></td>
    </tr>
    <tr>
      <td>Resolve Replication Gap</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>
    <tr>
      <td colspan="2">Step 5. Verify SQL Apply Mode Operation</td>
      <td>-</td>
      <td>-</td>
    </tr>      
    <tr>
      <td>Step 6. Restore Property Settings</td>
      <td>Disable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
    </tr>
    <tr>
      <td colspan="2">Step 7. Service Distribution</td>
      <td>There are no services to migrate since this is an Active-Standby environment.</td>
      <td></td>
    </tr>
  </tbody>
</table> 

##### Active-Active Environment

Assume that Active1 is the local server where primary transactions occur during DDL statement execution.

<table border="1" cellpadding="5" cellspacing="0">
  <thead>
    <tr>
      <th colspan="2">Step</th>
      <th>Active1</th>
      <th>Active2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Step 1. Service Migration</td>
      <td>Service Migration</td>
      <td></td>
      <td>Migrate the service to Active1.</td>
    </tr>
    <tr>
      <td>Verify the service migration</td>
      <td></td>
      <td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
    </tr>
    <tr>
      <td>Step 2. Configure Properties</td>
      <td>Enable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>        
    </tr>
    <tr>
      <td colspan="2">Step 3. Set Session Replication Mode</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
    </tr>
    <tr>
      <td rowspan="6">Step 4. Execute the DDL Statement</td>
      <td>Resolve Replication Gap</td>
      <td></td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td></td>
      <td>ALTER TABLE T1 ADD COLUMN ( i3 INTEGER );</td>
    </tr>
    <tr>
      <td>Resolve Replication Gap</td>
      <td></td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
    </tr>      
    <tr>
      <td>Resolve Replication Gap</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td>ALTER TABLE T1 ADD COLUMN ( i3 INTEGER );</td>
      <td></td>
    </tr>
    <tr>
      <td>Resolve Replication Gap</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>
    <tr>
      <td colspan="2">Step 5. Verify SQL Apply Mode Operation</td>
      <td>-</td>
      <td>-</td>
    </tr>      
    <tr>
      <td>Step 6. Restore Property Settings</td>
      <td>Disable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
    </tr>
    <tr>
      <td colspan="2">Step 7. Service Distribution</td>
      <td>Distribute the service to Active2.</td>
      <td></td>
    </tr>
  </tbody>
</table>




# 5. Executing DDL Synchronization

## Overview

DDL Synchronization is a feature that replicates the DDL statements performed on the replication target at the local server to the remote server in the same manner.

When DDL Synchronization is performed, transactions operate synchronously. If the DDL statement fails on either the primary transaction or the replicated transaction, the DDL statement will fail. Additionally, the replication target tables on both the local and remote servers will be locked, restricting transaction access.

### DDL Synchronization Properties

DDL Synchronization can be enabled by activating the related property.

| Property             | Description                              | Default |
| -------------------- | ---------------------------------------- | ------- |
| REPLICATION_DDL_SYNC | Enables the DDL Synchronization feature. | 0       |

### Execution Conditions

To use the DDL Synchronization feature, the following conditions must be met:

- Replication must be started on both the local and remote servers.
- The replication protocol version must be the same on both the local and remote servers.
- The name and owner of the replication target on both the local and remote servers must be the same.

### Restrictions

The following replication objects or targets cannot perform DDL Synchronization:

- Replication objects in EAGER mode
- Partitioned Table with global non-partitioned indexes
- Replication objects with the [PROPAGATION role](https://github.com/ALTIBASE/Documents/blob/master/Manuals/Altibase_trunk/kor/Replication%20Manual.md#propagation-%EB%A1%A4) specified
- Replication objects with [recovery options](#) enabled

The following statements cannot be replicated through DDL Synchronization:

- Rebuilding index partitions
- Granting and revoking privileges
- Creating and dropping triggers

## How to Perform DDL Synchronization

This section explains how to perform DDL Synchronization. For more detailed procedures, refer to the [DDL Synchronization Example](#ddl-synchronization-example).

In the procedure below, we assume that the server performing the DDL statement is the local server, and the server where DDL synchronization is performed is the remote server. Additionally, we assume that replication has been started on both servers.

#### Step 1. Service Migration

1. Migrate the service to the local server where the DDL statement will be executed.

2. Verify that the service has been successfully migrated.

   On the remote server, execute the following query and confirm that the result is 0.

   ```sql
   SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();
   ```

#### Step 2. Configure Properties

Set the properties required for executing DDL statements on local and remote servers.

When setting `REPLICATION_DDL_SYNC`, note that `ALTER SESSION` should be used on the local server, while `ALTER SYSTEM` should be used on the remote server.

- Properties to be modified on the local server

```sql
ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;
ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;
ALTER SESSION SET REPLICATION_DDL_SYNC = 1;
```

- Properties to be modified on the romote server

```sql
ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;
ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;
ALTER SYSTEM SET REPLICATION_DDL_SYNC=1;
ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;
```

#### Step 3. Set Session Replication Mode

On the local server, set the session's replication mode[^3] so that it follows the configuration of the replication object.

```sql
ALTER SESSION SET REPLICATION = DEFAULT;
```

#### Step 4. Execute the DDL Statement

1. Before executing the DDL statement, run the following query on both the local and remote servers to resolve any remaining replication gaps.

   ```sql
   ALTER REPLICATION replication_name FLUSH;
   ```

2. Execute the DDL statement on the local server.

#### Step 5. Restore Property Settings

Once the DDL Synchronization is completed, the properties used for DDL synchronization should be reverted to their default values immediately.

- Revert to default on the local server

```sql
ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0; 
ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;   
ALTER SESSION SET REPLICATION_DDL_SYNC = 0;
```

- Revert to default on the remote server

```sql
ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;
ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;
ALTER SYSTEM SET REPLICATION_DDL_SYNC = 0;
ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;
```

#### Step 6. Service Distribution

Redistribute the service back to its original configuration.

#### Operation Procedure Table

<table border="1" cellpadding="5" cellspacing="0">
  <thead>
    <tr>
      <th colspan="2">Step</th>
      <th>Local server</th>
      <th>Remote server</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Step 1. Service Migration</td>
      <td>Service Migration</td>
      <td></td>
      <td>Migrate Service to Local Server</td>
    </tr>
    <tr>
        <td>Verify the service migration</td>
        <td></td>
        <td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
    </tr>
    <tr>
      <td rowspan="4">Step 2. Configure Properties</td>
      <td>Enable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
    </tr>
    <tr>
      <td>Enable SQL Apply Mode</td>
      <td></td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
    </tr>
    <tr>
      <td>Enable DDL Synchronization</td>
      <td>ALTER SESSION SET REPLICATION_DDL_SYNC = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_SYNC = 1;</td>
    </tr>
    <tr>
      <td colspan="2">Step 3. Set Session Replication Mode</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
      <td></td>
    </tr>
    <tr>
      <td rowspan="4">Step 4. Execute the DDL Statement</td>
      <td>Resolve Replication Gap (Remote Server)</td>
      <td></td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>        
    </tr>        
    <tr>
      <td>Resolve Replication Gap (Local Server)</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr> 
    <tr>      
      <td>Execute the DDL Statement</td>
      <td>Execute the DDL Statement</td>
      <td></td>
    </tr>
     <tr>
      <td>Resolve Replication Gap (Local Server)</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>      
    <tr>
      <td rowspan="4">Step 5. Restore Property Settings</td>
      <td>Disable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
    </tr>
    <tr>
      <td>Disable DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
    </tr>    
    <tr>
      <td>Disable SQL Apply Mode</td>
      <td></td>
      <td>ALTER SESSION SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
    </tr>      
    <tr>
      <td>Disable DDL Synchronization</td>
      <td>ALTER SESSION SET REPLICATION_DDL_SYNC = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_SYNC = 0;</td>
    </tr>
    <tr>
      <td colspan="2">Step 6. Service Distribution</td>
      <td>Distribute Service to Remote Server</td>
      <td></td>
    </tr>
  </tbody>
</table>


## DDL Synchronization Example

This section introduces three examples of performing DDL statements on replication targets using the DDL Synchronization feature.

In all examples, the following terms are used:

- **Local Server**: The server where the DDL statement is executed.
- **Remote Server**: The server where DDL synchronization is performed.

Additionally, all examples assume that replication has already been started on both servers.

### Example 1: TRUNCATE Statement Synchronization

This example demonstrates the process of executing a TRUNCATE statement on the *t1* table on the local server, and how that statement is replicated to the remote server.

Here, it is assumed that the *t1* table is a replication target table included in the replication object *rep1*.

<table border="1" cellpadding="5" cellspacing="0">
  <thead>
    <tr>
      <th colspan="2">Step</th>
      <th>Local server</th>
      <th>Remote server</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Step 1. Service Migration</td>
      <td>Service Migration</td>
      <td></td>
      <td>Migrate Service to Local Server</td>
    </tr>
    <tr>
        <td>Verify the service migration</td>
        <td></td>
        <td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
    </tr>      
    <tr>
      <td rowspan="2">Step 2. Configure Properties</td>
      <td>Enable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
    </tr>
    <tr>
      <td>Enable DDL Synchronization</td>
      <td>ALTER SESSION SET REPLICATION_DDL_SYNC = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_SYNC = 1;</td>
    </tr>
    <tr>
      <td colspan="2">Step 3. Set Session Replication Mode</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
      <td></td>
    </tr>
    <tr>
      <td rowspan="4">Step 4. Execute the DDL Statement</td>
      <td>Resolve Replication Gap</td>
      <td></td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
    </tr>
    <tr>
      <td>Resolve Replication Gap</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td>TRUNCATE TABLE t1;</td>
      <td></td>
    </tr>
    <tr>
      <td>Resolve Replication Gap</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>           
    <tr>
      <td rowspan="2">Step 5. Restore Property Settings</td>
      <td>Disable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
    </tr>
    <tr>
      <td>Disable DDL Synchronization</td>
      <td>ALTER SESSION SET REPLICATION_DDL_SYNC = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_SYNC = 0;</td>
    </tr>
    <tr>
      <td colspan="2">Step 6. Service Distribution</td>
      <td>Distribute Service to Remote Server</td>
      <td></td>
    </tr>
  </tbody>
</table>

### Example 2: Replicating the Addition of a NOT NULL Constraint

This example demonstrates the process of adding a NOT NULL constraint to column *`c1`* of the *`t1`* table on the local server, and how that statement is replicated to the remote server.

Here, it is assumed that the *t1* table is a replication target table included in the replication object *rep1*.

<table border="1" cellpadding="5" cellspacing="0">
  <thead>
    <tr>
      <th colspan="2">Step</th>
      <th>Local server</th>
      <th>Remote server</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Step 1. Service Migration</td>
      <td>Service Migration</td>
      <td></td>
      <td>Migrate Service to Local Server</td>
    </tr>
    <tr>
        <td>Verify the service migration</td>
        <td></td>
        <td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
    </tr>
    <tr>
      <td rowspan="4">Step 2. Configure Properties</td>
      <td>Enable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
    </tr>
    <tr>
      <td>Enable SQL Apply Mode</td>
      <td></td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
    </tr>
    <tr>
      <td>Enable DDL Synchronization</td>
      <td>ALTER SESSION SET REPLICATION_DDL_SYNC = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_SYNC = 1;</td>
    </tr>
    <tr>
      <td colspan="2">Step 3. Set Session Replication Mode</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
      <td></td>
    </tr>
    <tr>
      <td rowspan="4">Step 4. Execute the DDL Statement</td>
      <td>Resolve Replication Gap</td>
      <td></td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
    </tr>      
    <tr>
      <td>Resolve Replication Gap</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td>ALTER TABLE t1 ALTER COLUMN ( c1 NOT NULL );</td>
      <td></td>
    </tr>  
    <tr>
      <td>Resolve Replication Gap</td>
      <td>ALTER REPLICATION rep1 FLUSH;</td>
      <td></td>
    </tr>       
    <tr>
      <td rowspan="4">Step 5. Restore Property Settings</td>
      <td>Disable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
    </tr>
    <tr>
      <td>Disable SQL Apply Mode</td>
      <td></td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
    </tr>
    <tr>
      <td>Disable DDL Synchronization</td>
      <td>ALTER SESSION SET REPLICATION_DDL_SYNC = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_SYNC = 0;</td>
    </tr>
    <tr>
      <td colspan="2">Step 6. Service Distribution</td>
      <td>Distribute Service to Remote Server</td>
      <td></td>
    </tr>
  </tbody>
</table>



### Example 3: Replicating DDL Statements in a Triple Replication Environment

The following example demonstrates how to add a column with a NOT NULL constraint to a replication target table in a triple replication environment.

The relevant replication information used in this example is as follows:

- Servers participating in the triple replication:
  - Local Server: The server where the DDL statement is executed.
  - Remote Server 1: The server where DDL synchronization is performed.
  - Remote Server 2: The server where DDL synchronization is performed.

- Replication Object Names:
  - *rep1*: Replication object between the local server and Remote Server 1
  - *rep2*: Replication object between the local server and Remote Server 2
  - *rep3*: Replication object between the Remote Server 1 and Remote Server 2
- Replication Target Table : *t1*

<table border="1" cellpadding="5" cellspacing="0">
  <thead>
    <tr>
      <th colspan="2">Step</th>
      <th>Local Server</th>
      <th>Remote Server 1</th>
      <th>Remote Server 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Step 1. Service Migration</td>
      <td>Service Migration</td>
      <td></td>
      <td>Migrate Service to Local Server</td>
      <td>Migrate Service to Local Server</td>        
    </tr>
    <tr>
        <td>Verify the service migration</td>
        <td></td>
        <td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
        <td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>        
    </tr>      
    <tr>
      <td rowspan="4">Step 2. Configure Properties</td>
      <td>Enable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 1;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 1;</td>
    </tr>
    <tr>
      <td>Enable SQL Apply Mode</td>
      <td></td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
    </tr>
    <tr>
      <td>Enable DDL Synchronization</td>
      <td>ALTER SESSION SET REPLICATION_DDL_SYNC = 1;</td>
      <td>ALTER SESSION SET REPLICATION_DDL_SYNC = 1;</td>
      <td>ALTER SESSION SET REPLICATION_DDL_SYNC = 1;</td>
    </tr>
    <tr>
      <td colspan="2">Step 3. Set Session Replication Mode</td>
      <td>ALTER SESSION SET REPLICATION = DEFAULT;</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td rowspan="4">Step 4. Execute the DDL Statement</td>
      <td>Resolve Replication Gap</td>
      <td></td>
      <td>ALTER REPLICATION rep1 FLUSH;<br>ALTER REPLICATION rep3 FLUSH;</td>
      <td>ALTER REPLICATION rep2 FLUSH;<br>ALTER REPLICATION rep3 FLUSH;</td>
    </tr>
    <tr>
      <td>Resolve Replication Gap</td>
      <td>ALTER REPLICATION rep1 FLUSH;<br>ALTER REPLICATION rep2 FLUSH;</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>Execute the DDL Statement</td>
      <td>ALTER TABLE t1 ALTER COLUMN ( c1 NOT NULL );</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>Resolve Replication Gap</td>
      <td>ALTER REPLICATION rep1 FLUSH;<br>ALTER REPLICATION rep2 FLUSH;</td>
      <td></td>
      <td></td>
    </tr>     
    <tr>
      <td rowspan="4">Step 5. Restore Property Settings</td>
      <td>Disable DDL Statement Execution</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE = 0;</td>
    </tr>
    <tr>
      <td>Set DDL Execution Level</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_ENABLE_LEVEL = 0;</td>
    </tr>
    <tr>
      <td>Disable SQL Apply Mode</td>
      <td></td>        
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
    </tr>
    <tr>
      <td>Disable DDL Synchronization</td>
      <td>ALTER SESSION SET REPLICATION_DDL_SYNC = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_SYNC = 0;</td>
      <td>ALTER SYSTEM SET REPLICATION_DDL_SYNC = 0;</td>
    </tr>
    <tr>
      <td colspan="2">Step 6. Service Distribution</td>
      <td>Distribute the service to Remote Server 1 and Remote Server 2</td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>


# 6. Fail-Over

The Fail-Over feature is provided so that a fault that occurs while a database is providing service can be overcome and service can continue to be provided as though no fault had occurred. This chapter explains the Fail-Over feature that is provided with Altibase, and how to use it.

### Fail-Over Overview

#### Concept

“Fail-Over” refers to the ability to overcome a fault that occurs while a database is providing service, so that service can continue to be provided as though no fault had occurred.

The kinds of faults that can occur include the case in which the DBMS server hardware itself develops a fault, the case in which the server’s network connection is interrupted, and the case in which a software error causes the DBMS to shut down abnormally. When any of the above kinds of fault occurs, Fail-Over makes it possible to connect to another server, so that service can be provided without interruption, and so that client applications are never aware that a fault has occurred.

There are two types of Fail-Over, distinguished from each other according to the time of failure cognition.

-   CTF (Connection Time Fail-Over)

-   STF (Service Time Fail-Over)

CTF refers to the case where the fault is noted at the time of connection to the DBMS, and connection is made to a DBMS on another available node rather than to the DBMS suffering from the fault, so that service can continue to be provided.

In the case of STF, in contrast, because a fault occurs while service is being provided after successful connection to the DBMS, reconnection is made to a DBMS on another available node, and session properties are restored, so that the business logic of the user’s application can continue to be used. Therefore, tasks currently being executed on the DBMS in which the fault occurred may need to be reexecuted.

With this kind of Fail-Over, in order to have confidence in the results of a task, the databases on the DBMS in which the fault occurred and the DBMS that is available to provide service must be guaranteed to be in exactly the same state and to contain exactly the same data.

In order to guarantee that the databases match, Altibase copies the database using Off-Line Replication. In Off-Line Replication, the Standby Server reads the logs from the Active Server so that it can harmonize its database with that on the Active Server.

Because one of the characteristics of replication is that the databases might not be in exactly the same state, we recommend that the Fail-Over Callback function be used to confirm that the databases match.

Fail-Over settings of Altibase include a Fail-Over property, which is set to TRUE to specify that Fail-Over is to be executed. Additionally, the Fail-Over Callback function can be used to check whether the databases match before Fail-Over is executed.

The three kinds of Fail-Over-related tasks that must be executed by the client application are summarized as follows:

-   The Fail-Over properties must be registered

-   The Fail-Over Callback function must be registered.

-   Additional tasks may be necessary depending on the result of callback

### Callback - JDBC

#### Fail-Over related Callback Interface

ABFailOverCallback interface is defined as below:

```
public interface ABFailOverCallback
{
	int FO_BEGIN	= 0;
	int FO_END	= 1;
	int FO_ABORT	= 2;
	int FO_GO	= 3;
	int FO_QUIT	= 4;

	int failOverCallback(Connection aConnection,
		   Object aAppContext,
		   int aFailOverEvent);
};
```

The meaning of the values is as follows: 

-   FO_BEGIN  
    FailOverCallback is notified of the start of STF (Service Time FailOver).

-   FO_END  
    FailOverCallback is notified of the success of STF.

-   FO_ABORT  
    FailOverCallback is notified of the failure of STF.

-   FO_GO  
    FailOverCallback sends this to JDBC so that STF can advance to the next step.

-   FO_QUIT  
    This is used to notify JDBC of the failure of FailOverCallback.

-   aAppContext  
    This includes information about any objects that the user intends to save. If there are no objects to be saved, this is set to NULL.

#### Fail-Over Process

The Fail-Over registration and handling process is as shown in the following figure.

![](media/Replication/Replication_eng.1.22.1.jpg)

[Figure 4-1] Fail-Over Registration and Handling Process

Fail-Over Callback must be registered by the user, and, once registered, during the Fail-Over process the Altibase User Library (for example, the JDBC and CLI libraries) communicates with client applications, as shown in the picture above.

If Fail-Over Callback is not registered, Fail-Over takes place without communication with the client application, and a trace log of the steps shown above is kept. In a replicated Altibase database environment, the use of callback is strongly recommended, so that Fail-Over Validation can be conducted.

![](media/Replication/Replication_eng.1.22.2.jpg)

1. After connecting to the database, the user registers Fail-Over Callback in the connection attributes.

2. The business logic is conducted in the client application. While the client application is running, if it receives an error message about a fault occurring in the DBMS hardware (including a network error), it calls the Altibase User Library so that Fail-Over can be conducted.

3. This client library sends a Fail-Over Start Event (FO_BEGIN) to the registered Fail-Over Callback. Fail-Over Callback returns information about whether Fail-Over will continue to progress. 
4. If Fail-Over Callback determines that the Fail-Over process should continue (FO_GO), executed SQL statements are closed, an available server is located, and the Altibase User Library connects and logs in to that database. Additionally, the properties of the previous session (autocommit mode, optimization settings, XA connection settings, etc.) are restored on the new server. 
5. When step number 4 is complete, Fail-Over Callback sends an event indicating that the Fail-Over process has been completed successfully (FO_END). 
6. Fail-Over Callback executes a query to ensure that the databases match (Fail-Over Validation). In a replicated database environment, it is essential to ensure that the databases match.

### Using Fail-Over

#### Registering Connection Properties

Once the Fail-Over connection properties have been registered, when a fault occurs, Altibase detects this and internally conducts the Fail-Over tasks according to the expressly specified connection properties.

The properties can be specified in the following two ways:

-   By specifying the Connection String when calling the API’s connection function

-   By specifying connection properties in the appropriate Altibase settings file (altibase_cli.ini)

##### Specifying the Connection String in a Client Application

When the connection function is executed in the client application, the following connection strings can be specified:

[JDBC]

```
Jdbc:Altibase://192.168.3.51:20300/mydb?AlternateServers=(192.168.3.54:20300,192.168.3.53:20300) &ConnectionRetryCount=3&ConnectionRetryDelay=3&SessionFailOver=on;
```

[ODBC, Embedded SQL]

```
DSN=192.168.3.51;UID=altibase;PWD=altibase;PORT_NO=20300;AlternateServers=(192.168.3.54:20300,192.168.3.53:20300);ConnectionRetryCount=3;ConnectionRetryDelay=5;SessionFailOver=on;
```

[PDO]

```
Server=192.168.3.51;Port=20300;AlternateServers=(192.168.3.54:20300,192.168.3.53:20300);ConnectionRetryCount=3;ConnectionRetryDelay=5;SessionFailOver=on
```

AlternateServer indicates servers to which connection can be made in the event of a fault, and is expressed in the form (IP Address1:Port1, IP Address2:Port2,...).

ConnectionRetryCount is the number of repeated connection attempts when a connection to an available server fails. It can be omitted, and the default value is 1.

ConnectionRetryDelay is the number of seconds to wait before attempting to reconnect if an available server connection fails. It can be omitted, and the default value is 1.

SessionFailOver indicates whether to perform a service time fail-over (STF). It can be omitted, and the default value is off. 

##### Specifying the Connection Properties in the Settings File

The Fail-Over connection settings can be specified in the Data Source portion of the altibase_cli.ini file, which is located in the \$ALTIBASE_HOME/conf directory, the $HOME directory, or the current directory of the relevant client application, and the DataSource name is specified in the Connection String of the connection function.

```
[MyDataSource1]
Server=192.168.3.51
Port=20300
User=altibase
Password=altibase
DataBase = mydb
AlternateServers=(192.168.3.54:20300,192.168.3.53:20300)
ConnectionRetryCount=3
ConnectionRetryDelay=5
SessionFailOver = off
```

The Connection String of the client application’s connection function appears as shown below, depending on the connection interface used by the client application.

-   JDBC  
    The data source name is specified as part of the Connection URL as follows:

```
Jdbc:Altibase://MyDataSource1//
```

-   ODBC, Embedded SQL  
    The data source name is specified in the DSN properties as follows. Settings are made in the odic.ini file in the same way that they are made in the altibase.cli.ini file.

```
DSN=MyDataSource1
```

-   PDO  
    The data source name is specified in the DSN properties as follows: 

```
altibase:MyDataSource1
```

#### Checking Whether Fail-Over Succeeded

Whether CTF (Connection Time Fail-Over) was successful can be quickly and easily determined merely by checking whether it is possible to connect to the database. In contrast, determining whether STF (Service Time Fail-Over) was successful involves checking for exceptions and errors.

For example, when using JDBC, a SQLException is caught, and the SQLException’s getSQLState() method is used to check the value of SQLStates.status. If this value is ES_08FO01, Fail-Over is determined to have been successful.

When using a CLI or ODBC, if the result of SQLPrepare, SQLExecute, SQLFetch or the like is an error, rather than SQL_SUCCESS, a statement handle is handed over to the SQLGetDiagRec function, and if the native error code that is returned in the 5th argument of this function has a diagnostic record equal to ALTIBASE_FAILOVER_SUCCESS, STF (Service Time Fail-Over) can be determined to have succeeded.

When using Embedded SQL, after executing the EXEC SQL command, if sqlca.sqlcode is not SQL_SUCCESS but ALTIBASE_FAILOVER_SUCCESS, this means that STF (Service Time Fail-Over) was successful.

The actual method of determining whether Fail-Over has succeeded varies according to the type of client application, as will be explained below.

In case of PDO, if the driver-specific error code is same as PDO::ALTIBASE_FAIL_SUCCESS, this means that STF (Service Time Fail-Over) was successful.

#### Writing Fail-Over Callback Functions

It is necessary to write a callback function to determine whether databases match when Fail-Over is executed. The method of writing Fail-Over Callback functions varies depending on the type of client application, but the basic structure is the same, and is as follows:

-   Define data structures related to Fail-Over 
-   Write Fail-Over Callback function bodies for handling Fail-Over-related events 
-   Write code to determine whether Fail-Over was successful

Either Fail-Over events are defined in the data structure definition, or else a defined interface (header file) is included in the data structure definition.

Various tasks must be conducted in response to Fail-Over-related events such as the start or completion of Fail-Over. Code for performing these tasks, including for example the task of checking whether the contents of databases match, is located in the callback function body.

Determining that Fail-Over has succeeded consists of the successful completion of Fail-Over and the successful execution of a Fail-Over callback function, and means that service that was suspended due to a fault can continue to be provided.

The actual method of writing callback functions is described below for various client application environments.

### Writing Callback in JDBC

#### Fail-Over related Callback Interface

To write a Fail-Over callback function in an application using JDBC, the user must write a class that implements the ABFailOverCallback interface provided by the Altibase JDBC driver. The ABFailOverCallback interface is defined as follows.

```
public interface ABFailOverCallback
{
	int FO_BEGIN	= 0;
	int FO_END	= 1;
	int FO_ABORT	= 2;
	int FO_GO	= 3;
	int FO_QUIT	= 4;

	int failOverCallback(Connection aConnection,
		   Object aAppContext,
		   int aFailOverEvent);
};
```

The meaning of the values is as follows:

-   FO_BEGIN  
    This event notifies Fail-Over callback that STF (Service Time FailOver) starts.

-   FO_END  
    This event notifies Fail-Over callback that the STF was successful.

-   FO_ABORT  
    This event notifies Fail-Over callback that the STF has failed.

-   FO_GO  
    This is the value that the user returns from the callback funciton to the library in order to proceed with the next step of STF.

-   FO_QUIT  
    This is the value that the user returns from the callback function to the library, meaning that the STF should not proceed.

-   aAppContext  
    This is an arbitrary object that the user wants to save. If there is no object to save, set it to null.
    
#### Writing Fail-Over Callback Functions

The MyFailOverCallback class, which implements the ABFailOverCallback Interface, must be written.

The tasks to be conducted in response to the FO_BEGIN and FO_END events, which are defined in the callback interface, must be handled by this class. That is to say, the required tasks for each of the Fail-Over events are described here.

For example, when the FO_BEGIN event occurs, code for handling tasks that are required before Fail-Over starts is provided, and when the FO_END event occurs, code for handling tasks that are required after Fail-Over ends and before service resumes is provided. One concrete example is the code that is used to check whether the data are consistent between available databases when the FO_END event occurs.

```
public class MyFailOverCallback implements ABFailOverCallback
{
    public int failOverCallback(Connection aConnection,
                               Object    aAppContext,
                               int        aFailOverEvent)
    {
        Statement sStmt  = null;
        ResultSet sRes  =  null;

        switch (aFailOverEvent)
        {
            case ABFailOverCallback.FO_BEGIN:
                System.out.println(“FailOver Started .... “);
                break;

            case ABFailOverCallback.FO_END:
                try
                {
                    sStmt = aConnection.createStatement();
                }
                catch( SQLException ex1 )
                {
                    try
                    {
                        sStmt.close();
                    }
                    catch( SQLException ex3 )
                    {
                    }
                    return ABFailOverCallback.FO_QUIT;
                } //catch  SQLException ex1

                try
                {
                    sRes = sStmt.executeQuery("select 1 from dual");
                    while(sRes.next())
                    {
                        if(sRes.getInt(1) == 1 )
                        {
                            break;
                        }
                    }//while;
                }
                catch ( SQLException ex2 )
                {
                    try
                    {
                        sStmt.close();
                    }
                    catch( SQLException ex3 )
                    {
                    }
                    return ABFailOverCallback.FO_QUIT;
                }//catch
                break;
        }//switch
        return ABFailOverCallback.FO_GO;
    }
}
```

Furthermore, the MyFailOverCallback class defined above is used to create a callback object.

```
MyFailOverCallback sMyFailOverCallback = new MyFailOverCallback();
Properties sProp = new Properties();
String sURL = "jdbc:Altibase://192.168.3.51:20300+"/mydb?AlternateServers=(192.168.3.54:20300,192.168.3.53:20300)&connectionRetryCount=3&
connectionRetryDelay=10&sessionFailOver=on";
```

The created callback object is registered with the connection object. 

```
((ABConnection)sCon).registerFailOverCallback(sMyFailOverCallback,null);
```

#### Checking Whether Fail-Over Succeeded

Checking whether Fail-Over, particularly STF (Service Time Fail-Over), was successful is conducted using SQLException. An SQLException is caught, and the SQLException’s getSQLState() method is used to check the value of SQLStates.status. If this value is ES_08FO01, Fail-Over is determined to have been successful.

The following example demonstrates how to check whether Fail-Over was successful.

```
while(true)
{
    try
    {
        sRes = sStmt.executeQuery(“SELECT C1 FROM T1”);
        while( sRes.next() )
        {
            System.out.println( "VALUE : " + sRes.getString(1)  );
        }//while
        break;
    }
    catch ( SQLException e )
    {
        if(e.getSQLState().equals(SQLStates.status[SQLStates.ES_08FO01])  == true)
        {
            continue;
        }
        System.out.println( "EXCEPTION : " + e.getMessage() );
        break;
    }
}
```

#### Sending Fail-Over Connection Settings to WAS

The Fail-Over property settings are added to the URL portion as follows:

```
"jdbc:Altibase://192.168.3.51:20300+"/mydb?AlternateServers=(128.1.3.53:20300,128.1.3.52:20300)&connectionRetryCount=3&connectionRetryDelay=10&sessionFailOver=on";
```

#### Example

When the callback functions defined above are used, client applications are authored as seen below. 

Please refer to the following example, which is included with the Altibase package and should have been installed in $ALTIBASE_HOME/sample/JDBC/Fail-Over/FailOverCallbackSample.java

When Fail-Over is completed, whether Fail-Over was successful is checked using SQLStates. The value of the element at index SQLStates.ES_08FO01 in the SQLStates.status array indicates that Fail-Over was successful, and that the client application can resume its tasks and service can be provided again

```
class   FailOverCallbackSample
{

    public static void main(String args[])  throws Exception
    {
        //---------------------------------------------------
        // Initialization
        //---------------------------------------------------
        // AlternateServers is the available node property
        String sURL = "jdbc:Altibase://127.0.0.1:" +
args[0]+"/mydb?AlternateServers=(128.1.3.53:20300,128.1.3.52:20301)&
ConnectionRetryCount=100&ConnectionRetryDelay=100&SessionFailOver=on";
        
        try
        {
            Class.forName("Altibase.jdbc.driver.AltibaseDriver");
        }
        catch ( Exception e )
        {
            System.err.println("Can't register Altibase Driver\n");
            return;
        }

        //---------------------------------------------------
        // Test Body
        //---------------------------------------------------

        //-----------------------
        // Preparation
        //-----------------------

        Properties sProp = new Properties();
        Connection sCon;
        PreparedStatement  sStmt = null;
        ResultSet sRes = null ;
        sProp.put("user", "SYS");
        sProp.put("password", "MANAGER");
        
        MyFailOverCallback sMyFailOverCallback = new MyFailOverCallback();
        sCon = DriverManager.getConnection(sURL, sProp);

        //FailOverCallback is registered.
        ((ABConnection)sCon).registerFailOverCallback(sMyFailOverCallback, null);

        // Programs must be written in the following form in order to support Session Fail-Over.
        /*
          while (true)
          {
            try
            {
            
            }
            catch(  SQLException e)
            {
                //Fail-Over occurs
                if(e.getSQLState().equals(SQLStates.status[SQLStates.ES_08FO01])  == true)
                {
                    continue;
                }
                System.out.println( "EXCEPTION : " + e.getMessage() );
                break;

            }       
             break;
          } // while
        */
        
        while(true)
        {
            try 
            {
                sStmt = sCon.prepareStatement("SELECT C1 FROM T2   ORDER BY C1");
                sRes = sStmt.executeQuery();
                while( sRes.next() )
                {
                    System.out.println( "VALUE : " + sRes.getString(1)  );
                }//while
            }
            
            catch ( SQLException e )
            {
                //FailOver Occurs
                if(e.getSQLState().equals(SQLStates.status[SQLStates.ES_08FO01])  == true)
                {
                    continue;
                }
                System.out.println( "EXCEPTION : " + e.getMessage() );
                break;
            }
            break;

        }
        sRes.close();
        //---------------------------------------------------
        // Finalize
        //---------------------------------------------------
        
        sStmt.close();
        sCon.close();
    }
}
```

### SQLCLI

In this section, the structure of sqlcli.h and the Fail-Over related constants that are declared therein will be examined, and how to register Fail-Over Callback will be explained with reference to an example.

#### Related Data Structures

The prototype of the Fail-Over callback function, used for communication between the client application and the CLI library during STF (Service Time Fail-Over), is shown below.

```
typedef  SQLUINTEGER  SQL_API (*SQLFailOverCallbackFunc)
           (SQLHDBC         aDBC,
            void            *aAppContext,
            SQLUINTEGER     aFailOverEvent);
```

aDBC is the SQLHDBC created by the client application using SQLAllocHandle.

aAppContext is a pointer, sent to the CLI library at the time of registration of FailOverCallbackContext, pointing to an object that the user wishes to save. When Fail-Over callback is called at the time of STF (Service Time FailOver), it is sent again to Fail-Over callback.

aFailOverEvent can be set to the following values, which have the meanings described below.

-   **ALTIBASE_FO_BEGIN: 0**  
    Fail-Over callback is notified of the start of STF (Service Time FailOver).

-   **ALTIBASE_FO_END: 1**  
    Fail-Over callback is notified of the success of STF (Service Time FailOver).

-   **ALTIBASE_FO_ABORT: 2**  
    Fail-Over callback is notified of the failure of STF (Service Time FailOver).

-   **ALTIBASE_FO_GO: 3**  
    Fail-Over callback sends aFailOverEvent to the CLI library so that STF can advance to the next step.
    
-   **ALTIBASE_FO_QUIT: 4**  
    Fail-Over callback sends aFailOverEvent to the CLI library to prevent STF from advancing to the next step.

The structure of SQLFailOverCallbackContext used when registering a fail-over callback in a CLI application is as follows:

```
typedef   struct SQLFailOverCallbackContext
{
    SQLHDBC                    mDBC;
    void                       *mAppContext;
    SQLFailOverCallbackFunc    mFailOverCallbackFunc;
}SQLFailOverCallbackContext;
```

In the case of CLI, mDBC can be set to NULL.

mAppContext includes information about any objects that the user intends to save. If there are no objects to be saved, this is set to NULL

mFailOverCallbackFunc is the name of the user-defined FailOverCallback function.

#### Registering Fail-Over

As can be seen below, the process of Fail-Over registration involves the creation of a SQLFailOverCallbackContext object, and after connection to the database is successful, FailOverCallbackContext is filled in with values.

The following is an example of Fail-Over registration.

```
SQLFailOverCallbackContext  sFailOverCallbackContext;
...... <<some code omitted here>>
 /* connect to server */
sRetCode = SQLDriverConnect(sDbc, NULL,
SQLCHAR*)”DSN=127.0.0.1;UID=unclee;PWD=unclee;PORT_NO=20300;
AlternateServers=(192.168.3.54:20300,192.168.3.53:20300);ConnectionRetryCount=3;
ConnectionRetryDelay=5;SessionFailOver=on;”),
SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);

sFailOverCallbackContext.mDBC = NULL;
sFailOverCallbackContext.mAppContext = NULL;
sFailOverCallbackContext.mFailOverCallbackFunc = myFailOverCallback;
sRetCode = SQLSetConnectAttr(sDbc,ALTIBASE_FAILOVER_CALLBACK,
                                 (SQLPOINTER)&sFailOverCallbackContext, 0);
```

The contents of myFailOverCallback are as follows.

```
SQLUINTEGER  myFailOverCallback(SQLHDBC aDBC,
void *aAppContext,
SQLUINTEGER aFailOverEvent)
{
    SQLHSTMT 	sStmt = SQL_NULL_HSTMT;
    SQLRETURN   	sRetCode;
    SQLINTEGER    	sVal;
    SQLLEN            	sLen;
    SQLUINTEGER 	sFailOverIntension = ALTIBASE_FO_GO;

    switch(aFailOverEvent)
    {
        case ALTIBASE_FO_BEGIN:                      // Start Fail-Over
            break;
        case ALTIBASE_FO_END:
            sRetCode = SQLAllocStmt( aDBC,&sStmt);
            if(sRetCode != SQ_SUCCESS)
            {
                 printf("FailOver-Callback SQLAllocStmt Error ");
                 return ALTIBASE_FO_QUIT;
            } 
            sRetCode = SQLBindCol(sStmt, 1, SQL_C_SLONG , &sVal,0,&sLen);
            if(sRetCode != SQ_SUCCESS)
            {
                 printf("FailOver-Callback SQLBindCol");
                 return ALTIBASE_FO_QUIT;
             } 
            sRetCode =  SQLExecDirect(sStmt, (SQLCHAR *) "SELECT 1 FROM DUAL", 
                                          SQL_NTS);
            if(sRetCode != SQ_SUCCESS)
            {
                 printf("FailOVer-Callback SQLExecDirect");
                 return ALTIBASE_FO_QUIT;
            }
            while ( (sRetCode  = SQLFetch(sStmt)) != SQL_NO_DATA )
            {
                if(sRetCode != SQL_SUCCESS)
                {
                     printf("FailOver-Callback SQLBindCol");
                     sFailOverIntension =  ALTIBASE_FO_QUIT;
                     break;
                }
                printf("FailOverCallback->Fetch Value = %d \n",sVal );
                fflush(stdout);
            }

            sRetCode = SQLFreeStmt( sStmt, SQL_DROP );
            ATC_TEST(sRetCode,"SQLFreeStmt");
            break;

        default:
            break;
    }//switch 
    return  sFailOverIntension;
 }//myFailOverCallback
```

#### Checking Whether Fail-Over Succeeded

If the result of SQLPrepare, SQLExecute, SQLFetch or the like is an error, rather than SQL_SUCCESS, a statement handle is handed over to SQLGetDiagRec, and if aNativeError has a diagnostic record equal to ALTIBASE_FAILOVER_SUCCESS, STF (Service Time Fail-Over) can be determined to have succeeded.

The following example demonstrates how to check whether STF (Service Time Fail-Over) was successful.

```
UInt isFailOverErrorEvent(SQLHSTMT aStmt)
{
    SQLRETURN 	rc;
    SQLSMALLINT 	sRecordNo;
    SQLCHAR     	sSQLSTATE[6];
    SQLCHAR     	sMessage[2048];
    SQLSMALLINT 	sMessageLength;
    SQLINTEGER  	sNativeError;
    UInt        	sRet = 0;
    sRecordNo = 1;
    while ((rc = SQLGetDiagRec(SQL_HANDLE_STMT,
                                 aStmt,
                                 sRecordNo,
                                 sSQLSTATE,
                                 &sNativeError,
                                 sMessage,
                                 sizeof(sMessage),
                                 &sMessageLength)) != SQL_NO_DATA)
    {
        sRecordNo++;
        if(sNativeError == ALTIBASE_FAILOVER_SUCCESS)
        {
            sRet = 1;
            break;
        }
    }
    return sRet;
}
```

The following example shows that when a network error occurs while SQLExecDirect is being executed, whether STF (Service Time FailOver) was successful is checked, and it is re-executed if necessary (in a prepare/execute environment, re-execution would have to start at the prepare stage).

```
retry:
    sRetCode = SQLExecDirect(sStmt, 
(SQLCHAR *) "SELECT C1 FROM T2 WHERE C2 > ? ORDER BY C1", 
SQL_NTS);
    if(sRetCode != SQL_SUCCESS)
    {
        if(isFailOverErrorEvent(sStmt) == 1)
        {
            goto retry;
        }
        else
        {
            printf(“Error While DirectExeute....”);
            exit(-1).
        }
    }
```

#### Example

##### Environment Settings

To implement the example, a data source called Test1 is described in altibase_cli.ini as follows:

```
[ Test1  ]
Server=192.168.3.53
Port=20300
User=altibase
Password= altibase
DataBase = mydb
AlternateServers=(192.168.3.54:20300,192.168.3.53:20300)
ConnectionRetryCount=3
ConnectionRetryDelay=5
SessionFailOver = on
```

Additionally, the FailOverCallback function uses myFailOverCallback, which was described above.

When STF (Service Time Fail-Over) takes place, if it is successful, execution must be repeated starting with SQLPrepare (in the case of SQLDirectExecute, the prepare process is not necessary, and only SQLDirectExecute need be re-executed).

If STF (Service Time Fail-Over) occurs while data are being fetched, it will be necessary to call SQLCloseCursor and start over again from the prepare process (in the case of SQLDirectExecute, the prepare process is not necessary, and only SQLDirectExecute will need to be re-executed).

##### Sample Code

To view the complete contents of this example, please refer to $ALTIBASE_HOME/sample/SQLCLI/Fail-Over/FailOverCallbackSample.cpp.

```
#define ATC_TEST(rc, msg) if( ((rc)&(~1))!=0) { printf(msg); exit(1); }
//STF(Service Time FailOver) was successful.
UInt isFailOverErrorEvent(SQLHDBC aDBC,SQLHSTMT aStmt)
{
    SQLRETURN 	rc;
    SQLSMALLINT	sRecordNo;
    SQLCHAR   	sSQLSTATE[6];
    SQLCHAR   	sMessage[2048];
    SQLSMALLINT	sMessageLength;
    SQLINTEGER	sNativeError;
    UInt      		sRet = 0;
    sRecordNo = 1;

    while ((rc = SQLGetDiagRec(SQL_HANDLE_STMT, aStmt,
                                 sRecordNo, sSQLSTATE,
                                 &sNativeError,  sMessage,
                                 sizeof(sMessage),
                                 &sMessageLength)) != SQL_NO_DATA)
    {
        sRecordNo++;
        if(sNativeError == ALTIBASE_FAILOVER_SUCCESS)
        {
            sRet = 1;
            break;
        }
    }
    return sRet;
}

int main( SInt argc, SChar *argv[])
{
    SChar		sConnStr[BUFF_SIZE] = {0};
    SQLHANDLE   	sEnv  = SQL_NULL_HENV;
    SQLHANDLE   	sDbc  = SQL_NULL_HDBC;
    SQLHSTMT    	sStmt = SQL_NULL_HSTMT;
    SQLINTEGER  	sC2;
    SQLRETURN  	sRetCode;
    SQLINTEGER  	sInd;
    SQLINTEGER  	sValue;
    SQLLEN     	sLen;
    UInt        	sDidCreate = 0;
    SChar       	sBuff[BUFF_SIZE2];
    SChar       	sQuery[BUFF_SIZE];

    SQLFailOverCallbackContext  sFailOverCallbackContext;
    snprintf(sConnStr, sizeof(sConnStr), "DSN=Test1”);
    sprintf(sQuery,"SELECT C1 FROM T2  WHERE C2 > ? ORDER BY C1");
    sRetCode = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &sEnv);
    ATC_TEST(sRetCode,"ENV");
    sRetCode = SQLAllocHandle(SQL_HANDLE_DBC, sEnv, &sDbc);
    ATC_TEST(sRetCode,"DBC");
    /* connect to server */
    sRetCode = SQLDriverConnect(sDbc, NULL, (SQLCHAR *)sConnStr,
                                    SQL_NTS, NULL, 0, NULL,
                                SQL_DRIVER_NOPROMPT);
    ATC_TEST(sRetCode,"SQLDriverConnect");
    sRetCode = SQLAllocStmt( sDbc,&sStmt);
    ATC_TEST(sRetCode,"SQLAllocStmt");
    sRetCode = SQLBindCol(sStmt, 1, SQL_C_CHAR , sBuff,BUFF_SIZE2,&sLen);
    ATC_TEST(sRetCode,"SQLBindCol");
    sRetCode = SQLBindParameter(sStmt, 1, SQL_PARAM_INPUT,
                                    SQL_C_SLONG, SQL_INTEGER,
                                    0, 0, &sC2, 0, NULL);
    ATC_TEST(sRetCode,"SQLBindParameter");
    sFailOverCallbackContext.mDBC = NULL;
    sFailOverCallbackContext.mAppContext = &sFailOverDirection;
    sFailOverCallbackContext.mFailOverCallbackFunc = myFailOverCallback;
    sRetCode = SQLSetConnectAttr(sDbc,ALTIBASE_FAILOVER_CALLBACK,
                                     (SQLPOINTER)&sFailOverCallbackContext,0);
    ATC_TEST(sRetCode,"SQLSetConnectAttr");
  retry:
    sRetCode = SQLPrepare(sStmt, (SQLCHAR *)sQuery, SQL_NTS);
    if(sRetCode != SQL_SUCCESS)
    {
        // If STF was successful, start over again from the prepare stage.
        if(isFailOverErrorEvent(sDbc,sStmt) == 1)
        {
            goto retry;
        }
        else
        {
            ATC_TEST(sRetCode,"SQLPrepare");
        }
    }
    sC2 = 0;
    sRetCode =  SQLExecute(sStmt);
    if(sRetCode != SQL_SUCCESS)
    {
         // If STF was successful, start over again from the prepare stage.
        if(isFailOverErrorEvent(sDbc,sStmt) == 1)
        {
            goto retry;
        }
        else
        {
            ATC_TEST(sRetCode,"SQLExecDirect");
        }
    }

    while ( (sRetCode  = SQLFetch(sStmt)) != SQL_NO_DATA )
    {
        if(sRetCode != SQL_SUCCESS)
        {
            if(isFailOverErrorEvent(sDbc,sStmt) == 1)
            {
                //If STF occurs during a fetch operation, it is absolutely essential to call SQLCloseCursor. 
                SQLCloseCursor(sStmt);
                goto retry;
            }
            else
            {
                ATC_TEST(sRetCode,"SQLExecDirect");
            }
        }
        printf("Fetch Value = %s \n", sBuff);
        fflush(stdout);
    }
    sRetCode = SQLFreeStmt( sStmt, SQL_DROP );
    ATC_TEST(sRetCode,"SQLFreeStmt");
    sRetCode = SQLDisconnect(sDbc);
    ATC_TEST(sRetCode,"Disconnect()");
    sRetCode = SQLFreeHandle(SQL_HANDLE_DBC, sDbc);
    ATC_TEST(sRetCode,"Free HDBC");
    sRetCode = SQLFreeHandle(SQL_HANDLE_ENV, sEnv);
    ATC_TEST(sRetCode,"Free HENV");
}
```

### Embedded SQL

Because the Fail-Over data structures used here are the same as those used in CLI, and because the structure of an ESQLC (Embedded SQL in C) application is similar to that of a CLI application, only the features unique to ESQLC will be described here

#### Registering Fail-Over Callback Functions

Because SQLHDBC of CLI cannot be directly checked in an Embedded SQL program, the process of registering a Fail-Over callback function is as shown below.

FailOverCallbackContext is declared in the declaration section.

```
EXEC SQL BEGIN DECLARE SECTION;
SQLFailOverCallbackContext sFailOverCallbackContext;
EXEC SQL END DECLARE SECTION;
```

FailOverCallbackContext is filled in with values.

```
sFailOverCallbackContext.mDBC = NULL;
sFailOverCallbackContext.mAppContext = NULL;
sFailOverCallbackContext.mFailOverCallbackFunc = myFailOverCallback;
```

myFailOverCallback is the function that was seen in the CLI Fail-Over example above, only the CLI function and Os function need to be written, and Embedded SQL commands cannot be used.

The following shows how a Fail-Over Callback function is registered in an Embedded SQL statement.

```
EXEC SQL [AT CONNECTUON-NAME] REGISTER FAIL_OVER_CALLBACK :sFailOverCallbackContext;
```

#### Checking Whether Fail-Over Succeeded

After the EXEC SQL command is executed, if the result of sqlca.sqlcode is ALTIBASE_FAILOVER_SUCCESS, rather than SQL_SUCCESS, then STF (Service Time Fail-Over) can be determined to have succeeded.

The following example demonstrates how to check whether STF (Service Time Fail-Over) was successful.

```
re-execute:
    EXEC SQL INSERT INTO T1 VALUES( 1 );
    if (sqlca.sqlcode != SQL_SUCCESS)
    {
        if (sqlca.sqlcode == ALTIBASE_FAILOVER_SUCCESS)
        {
            goto re-execute;
        }//if
        else
        {
            printf("SQLCODE                : %d\n", SQLCODE);
            printf("sqlca.sqlerrm.sqlerrmc : %s\n", sqlca.sqlerrm.sqlerrmc);
            printf("%d rows inserted\n", sqlca.sqlerrd[2]);
             printf("%d times insert success\n\n", sqlca.sqlerrd[3]);
       }//else
    }
```

#### Example 1

```
main()
{
    EXEC SQL BEGIN DECLARE SECTION;
    SQLFailOverCallbackContext sFailOverCallbackContext;
    char sUser[10];
    char sPwd[10];
    char sConnOpt[1024];
    EXEC SQL END DECLARE SECTION;

    strcpy(sUser, "SYS");
    strcpy(sPwd, "MANAGER");
    sprintf(sConnOpt,”DSN=127.0.0.1;UID=altibase;PWD= altibase;PORT_NO=20300;
          AlternateServers=(192.168.3.54:20300,192.168.3.53:20300);ConnectionRetryCount=3;
          ConnectionRetryDelay=5;SessionFailOver=on;”” );

    EXEC SQL CONNECT :sUser IDENTIFIED BY :sPwd USING : sConnOpt;

    if (sqlca.sqlcode != SQL_SUCCESS)
    {
        printf("SQLCODE                : %d\n", SQLCODE);
        printf("sqlca.sqlerrm.sqlerrmc : %s\n", sqlca.sqlerrm.sqlerrmc);
        return 0;
    }
    else
    {
        printf("CONNECTION SUCCESS\n");
    }

    //FailOverCallbackContext is populated with values
    sFailOverCallbackContext.mDBC = NULL;
    sFailOverCallbackContext.mAppContext = NULL;
    sFailOverCallbackContext.mFailOverCallbackFunc = myFailOverCallback;
    // FailOverCallbackContext is registered.
    EXEC SQL  REGISTER FAIL_OVER_CALLBACK :sFailOverCallbackContext;

re-execute:
    EXEC SQL INSERT INTO T1 VALUES( 1 );
    if (sqlca.sqlcode != SQL_SUCCESS)
    {
        if (SQLCODE == EMBEDED_ALTIBASE_FAILOVER_SUCCESS)
        {
              goto re-execute;
         }//if
         else
         {
             printf("SQLCODE                : %d\n", SQLCODE);
             printf("sqlca.sqlerrm.sqlerrmc : %s\n", sqlca.sqlerrm.sqlerrmc);
             printf("%d rows inserted\n", sqlca.sqlerrd[2]);
             printf("%d times insert success\n\n", sqlca.sqlerrd[3]);
            return 0;
        }//else
    }
    EXEC  SQL DISCONNECT;
}
```

#### Example 2

This example demonstrates the use of a cursor. If Fail-Over occurs while a cursor is being used, EXEC SQL CLOSE RELEASE Cursor is executed, and the EXEC SQL DECLARE CURSOR statement is executed again to Prepare on the available server again.

```
retry:
   EXEC SQL DECLARE CUR1 CURSOR FOR SELECT C1 FROM T2 ORDER BY C1;
    if (sqlca.sqlcode == SQL_SUCCESS)
   {
         printf("DECLARE CURSOR SUCCESS.!!! \n");
    }
   else
   {
        if( SQLCODE  == EMBEDED_ALTIBASE_FAILOVER_SUCCESS)
        {
             printf("Fail-Over  SUCCESS !!! \n");
             goto retry;
        }
        else
        {
             printf("Error : [%d] %s\n\n", SQLCODE, sqlca.sqlerrm.sqlerrmc);
             return(-1);
        }
    }
    EXEC SQL OPEN CUR1;
    if (sqlca.sqlcode == SQL_SUCCESS)
    {
        printf("DECLARE CURSOR SUCCESS !!!\n");
    }
    else
    {
        if( SQLCODE  == EMBEDED_ALTIBASE_FAILOVER_SUCCESS)
        {
            printf("Fail-Over SUCCESS !!! \n");
            /* If a cursor is OPEN when Fail-Over occurs, the cursor must be closed and released */
            EXEC SQL CLOSE RELEASE CUR1;
            goto retry;
        }
        else
        {
             printf("Error : [%d] %s\n\n", SQLCODE, sqlca.sqlerrm.sqlerrmc);
             return(-1);
        }
    } //else 

    while(1)
    {
         EXEC SQL FETCH CUR1 INTO :sC1;
         if (sqlca.sqlcode == SQL_SUCCESS)
         {
              printf("Fetch Value = %s \n",sC1);
         }
         else if (sqlca.sqlcode == SQL_NO_DATA)
         {
              break;
         }
         else
         {
              if(SQLCODE == EMBEDED_ALTIBASE_FAILOVER_SUCCESS)
              {
                   printf("DECLARE CURSOR SUCCESS !!!");
                   /* If a fetch operation is underway when Fail-Over occurs, the cursor must be closed and released  */
                   EXEC SQL CLOSE RELEASE CUR1;
                   goto retry;
              }
              else
              {
                   printf("Error : [%d] %s\n\n", SQLCODE, sqlca.sqlerrm.sqlerrmc);
                   return(-1);
              }//else
         }//else
    }//while

    EXEC SQL CLOSE CUR1;
```

### PDO - Callback

#### Registering Fail-Over Callback

To register a Fail-over callback in an application using PDO, use the following method.

```
...
public bool PDO::setFailoverCallback(string $callback, mixed $app_context)
...
```

-   \$callback  
    This is the name of the function to register as a callback

-   \$app_context  
    This is an arbitrary variable to be used as a callback. The variable transferred to \$app_context is transferred as the \$context argument in the callback function. This value is for reference when performing user callback, so if it is not needed it, do not use it. This returns TRUE if the callback registration was successful and FALSE if it failed.

#### Fail-Over Callback Related Interfaces

In the application using PDO, FailOver Callback function is defined as below: 

```
function focbfunnc($db, $context, $event)
{
    // ...

    return PDO::ALTIBASE_FO_GO;
}
```

-   \$db  
    PDO object when Failover occurs

-   \$context  
    Arbitrary value referred in callback function, and it can be specified when registering callback.

-   \$event  
    Possible values for $event are as follows:

| event                  | Description |
| ---------------------- | ----------- |
| PDO::ALTIBASE_FO_BEGIN | STF Start   |
| PDO::ALTIBASE_FO_END   | STF Success |
| PDO::ALTIBASE_FO_ABORT | STF Fail    |

-   Callback returns of one the following values:

| Return Value          | Description     |
| --------------------- | --------------- |
| PDO::ALTIBASE_FO_GO   | STF Progressing |
| PDO::ALTIBASE_FO_QUIT | STF Stopped     |



#### Registering Fail-Over Callback

After a successful connection, the failover callback is specified. Examples are shown below: 

```
function focbfunc($db, $context, $event) {
    switch ($event) {
        case PDO::ALTIBASE_FO_BEGIN:
            if ($context == 1) {
                return PDO::ALTIBASE_FO_QUIT;
            }
            // ...
            break;

        case PDO::ALTIBASE_FO_END:
            // ...
            break;

        // ...
    }

    return PDO::ALTIBASE_FO_GO;
}

// ...

$db->setFailoverCallback('focbfunc', $appctx);
```

#### Checking Whether Fail-Over Succeeded

In case of Failover, if the driver-specific error code is PDO::ALTIBASE_FAILOVER_SUCCESS, STF is successful.

Failover only guarantees connection, so please be sure to check whether STF is succeeded and the execution is retried.

The following is an example of checking whether STF is succeeded and the execution is retried.

```
FailoverRetry:
try {
    $stmt = $db->prepare("SELECT c1 FROM T2 WHERE c2 ? ORDER BY c1");
    $stmt->bindParam(1, $sC2);

    $sC2 = 0;

    $stmt->execute();

    while (($row = $stmt->fetch()) !== FALSE) {
        // ...
    }
}
catch (PDOException $ex) {
    $errInfo = $ex->errorInfo;
    if ($errInfo[1] == PDO::ALTIBASE_FAILOVER_SUCCESS) {
        goto FailoverRetry;
    }
    else {
        // ...
    }
}
```

# 7. Sequence Replication

Altibase only supports replication of table objects by default. Thus, sequence replication means to create tables only for sequence replication, not copying the sequence itself. 

This chapter will cover the conditions and methods supporting the sequence replication.

### Sequence Replication

#### Overview 

Altibase sequence replication is a feature allowing the remote and local server to use an identical sequence even in the situation of fail-over. Thus, the same sequence and program sources can be used in an application.

Sequence replication should replicate the cache start value so that the sequence values are not duplicated on the two servers. The sequence equivalent to the cache size is stored in the memory to use, and if the stored sequence is used all, the cache size sequence is stored again in the memory.

The tables for sequence replication is internally created because Altibase replication only supports tables.

#### Usage Condition

It is required to configure the following property as shown below. please refer to Replication Reference and General Reference for more detailed information on this property.

```
REPLICATION_TIMESTAMP_RESOLUTION=1
```

The sequence option for the local and remote servers should be identical. Please refer to *SQL Reference* for more detailed information on the sequence option.

```
START WITH
INCREMENT BY
MAXVALUE
MINVALUE
CACHE
FLUSH CACHE
CYCLE
```

#### Syntax 

The major syntax for the sequence replication is as follows. Please refer to *SQL Reference* and *Replication Reference* for more detailed information.

##### Creating Sequence for Sequence Replication

If ENABLE SYNC TABLE option is specified, seq_name$ table for sequence replication is created. It is recommended to set cache size to 100 or more than 100. 

```
CREATE SEQUENCE user_name.seq_name START WITH 1 CACHE 100 ENABLE SYNC TABLE;
```

##### Creating Sequence Replication

The following syntax creates a replication object so that a table for sequence replication can be duplicated.

```
CREATE REPLICATION repl_name WITH 'remote_host_ip', remote_host_port_no FROM user_name.seq_name$seq TO user_name.seq_name$seq; 
```

##### Startup and Shutdown of Sequence Replication

The following syntax starts or shuts down the sequence replication.

```
ALTER REPLICATION repl_name START;
ALTER REPLICATION repl_name STOP;
```

##### Remove of Sequence Replication

After executing a query dropping a replication (DROP REPLICATION) or excluding a table from the replication target (ALTER TABLE table_name DROP COLUMN), the seq_name$seq table is removed.

```
ALTER SEQUENCE user_name.seq_name DISABLE SYNC TABLE; 
```

> #### Note:
>
> -   It is recommended to perform sequence replication in the active-standby environment. The sequence value can be duplicated due to the replication gap between servers if it is performed in the active-active environment.
> -   The larger the size of the sequence cache, the faster the sequence creation. The cache size should be modified in advance since it cannot be modified after the table the for sequence replication is created.
> 
> ```
>ALTER SEQUENCE username.seq_name CACHE 100;
> ALTER SEQUENCE user1.seq1 ENABLE SYNC TABLE;
> ```
> 
> -   The sequence replication with tables is not recommended. If a fail-over occurs in the situation of sequence replication delay caused by a table replication delay, sequence duplicate key error might occur. 
>   
> -   If the fail-over occurs, there would be blanks among key values since the remote server start from the next cache values when referencing the sequence.
>   
> -   Replication recreation, sequence recreation, and modification should be equivalently applied to all servers.
>

#### Example

The following example verifies the status of replication server when fail-over occurs during the execution of sequence replication.

| A Server                                                     | B Server                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| iSQL\> create sequence seq1 start with 1 increment by 1 cache 1000 enable sync table;<br/> Create success. | iSQL\> create sequence seq1 start with 1 increment by 1 cache 1000 enable sync table;<br/> Create success. |
| iSQL\> create replication rep1 with '192.168.1.2', 20002 from sys.seq1\$seq to sys.seq1\$seq;<br/> Create success. | iSQL\> create replication rep1 with '192.168.1.1', 20001 from sys.seq1\$seq to sys.seq1\$seq;<br/> Create success. |
| iSQL\> alter replication rep1 start;<br/> Alter success.     |                                                              |
| iSQL\> select LAST_SYNC_SEQ from seq1\$seq; LAST_SYNC_SEQ<br/> ----------------------<br/> 1<br/> 1 row selected. | iSQL\> select LAST_SYNC_SEQ from seq1\$seq; LAST_SYNC_SEQ<br/> ----------------------- <br/>1 <br/>1 row selected. |
| iSQL\> select seq1.nextval from dual; SEQ1.NEXTVAL<br/> ---------------------- <br/>1<br/> 1 row selected. |                                                              |
| iSQL\> select LAST_SYNC_SEQ from seq1\$seq; LAST_SYNC_SEQ<br/> ----------------------<br/> 1001<br/> 1 row selected. | iSQL\> select LAST_SYNC_SEQ from seq1\$seq; LAST_SYNC_SEQ<br/> ----------------------<br/> 1001<br/> 1 row selected. |
| iSQL\> select seq1.nextval from dual; SEQ1.NEXTVAL <br/>----------------------<br/> 2 <br/>1 row selected. <br/>iSQL\> select seq1.nextval from dual;<br/> SEQ1.NEXTVAL<br/> ----------------------<br/> 3<br/> 1 row selected. |                                                              |
| Fail-Over Occurrence                                         |                                                              |
|                                                              | iSQL\> select seq1.nextval from dual; SEQ1.NEXTVAL<br/> ----------------------<br/> 1001<br/> 1 row selected. <br/>iSQL\> select seq1.nextval from dual; SEQ1.NEXTVAL<br/> ---------------------- <br/>1002<br/> 1 row selected. <br/>iSQL\> select seq1.nextval from dual; SEQ1.NEXTVAL<br/> ----------------------<br/> 1003<br/> 1 row selected. |
| iSQL\> select LAST_SYNC_SEQ from seq1\$seq; LAST_SYNC_SEQ<br/> -------------------<br/> 2001<br/> 1 row selected. | iSQL\> select LAST_SYNC_SEQ from seq1\$seq; LAST_SYNC_SEQ <br/>---------------------- <br/>2001<br/> 1 row selected. |

# 8. ROLE

The role of replication is used to configure the system to perform special functions by assigning ROLE to replication.

Information about the replication role can be found through the ROLE column value in the V$SYS_REPLICATIONS_ meta table. Replication without a role implies basic 1:1 bidirectional replication between Altibase servers, with a ROLE column value of 0.

There are three types of replication roles: Log Analyzer, Propagable Logging, and Propagation. These roles can be specified when creating replication, and each has the following descriptions:

### Log Analyzer Role

To create replication as a Log Analyzer role, use the ANALYSIS keyword. The Log Analyzer role can be used together with the Propagation role. Please refer to the *Log Analyzer User’s Manual* For detailed information about the replication with Log Analyzer role.

### Propagation

Propagation refers to configuring the system to propagate replication through multiple nodes.

While normal replication marks the transactions performed by the receiver in the logs to prevent retransmission between each other, propagation allows transactions performed by the receiver to be propagated to other nodes. To leave the logs received by the receiver as replicable logs, the Propagable Logging role is required. Sending the replicable logs to other remote servers is performed by the sender in the replication with the Propagation role.

#### PROPAGABLE LOGGING Role

Replication with the PROPAGABLE LOGGING role performs propagable logging, which means logging the transactions that the receiver performed for propagating those transactions to other nodes. In other words, Replication with this role allows the sender specified as PROPAGATION role in the future to read the logs and propagate them to other nodes.

#### PROPAGATION Role

The sender with the PROPAGATION role reads not only the replication target logs but also the logs generated by propagable logging, and sends them to other nodes.

#### Cautions on Replication Propagation

* It is recommended not to use it with the RECOVERY option.
  * As the sender created with the PROPAGATION role propagates all logs propagable, the system design can become complex as it propagates the logs created by receivers with the RECOVERY option.
* Replication propagation should be configured in one direction only.
* Users should take care to avoid creating cycles in the propagation direction, as this can create a situation where changes in the logs are infinitely reapplied.
* A receiver using PROPAGABLE LOGGING leaves additional information such as PK when logging. Therefore, the receiver with PROPAGABLE LOGGING may have lower transaction performance than those without PROPAGABLE LOGGING.

# Appendix A: FAQ

### Replication FAQ

##### **Question**

I want to know how to resolve conflicts.

##### **Answer**

Please refer to the section "Troubleshooting" in Chapter 2.

##### **Question**

Is replication possible between two servers located on different local networks?

##### **Answer**

Yes, it's possible. However, because of the physical distance between two servers, replication performance may downgrade somewhat in accordance with bandwidth and latency.

##### **Question**

Can I execute ADD COLUMN on a replication target table?

##### **Answer**

Yes, you many execute DDL statements on replication target tables.

First, set the following property settings: set the REPLICATION_DDL_ENABLE property to 1, and, using the ALTER SESSION SET REPLICATION command, set the REPLICATION property to some value other than NONE.

For more detailed information, please refer to [Executing DDL Statements on Replication Target Tables](#).

##### **Question**

When one of two servers connected for replication goes down or offline and then comes back online, how can I check the current status of replication data to be sent to the other server? 

##### **Answer**

The replication gap, meaning the number of redo logs for which corresponding XLogs need to be sent but have not yet been sent, can be checked by querying the REP_GAP column in the V$REPGAP performance view. Performance views can also be used to check various other information related to replication execution.

##### **Question**

Is replication possible between two different kinds of servers? 

##### **Answer**

Yes, it's possible. The heterogeneous replication function of Altibase takes into account byte ordering, structure aligning, endian and bit count on both the Sender and Receiver in order to make replication between different kinds of servers possible.

To achieve this, when XLOGs are sent or received, the Sender thread adds data to be sent to a transmission buffer, and the Receiver thread receives data from a reception buffer in the same order in which it was sent by the Sender thread. 

However, when performing replication between heterogeneous servers, if the byte order is different, the necessary operation of changing the byte order will entail a reduction in performance.

##### **Question**

Can I add or delete tables while replication is active? 

##### **Answer**

This is impossible while replication is underway. To add or delete replication target tables, it is first necessary to stop replication.

##### **Question**

Can I perform replication between memory and disk tables? 

##### **Answer**

Yes, it's possible.

# Appendix B: Standard DDL Execution Procedure

This section explains how to perform DDL statements on replication targets without setting any specific replication properties.

### Prerequisites

This procedure assumes the following conditions:

- All replication properties related to DDL execution are set to their default values.
- Replication has been started on both servers.

### **Cautions**

- It is essential to stop services on the Active server.
- If the service on the Active server is not stopped before executing the DDL statement, data inconsistency may occur if the primary transaction is triggered simultaneously with the execution of the DDL statement.

This section describes how to execute DDL statements based on whether **it is possible or impossible to stop the service on the replication target server.**

## Environment Where Service Stop is Possible

In environments where the operation of all replication target servers can be halted, the following steps can be followed to execute DDL statements.

### Step 1: Stop the Service

1. Stop the service on the Active server.

2. Verify that the service has been stopped by checking the database session on the Active server.

   ```sql
   SELECT COUNT(*) FROM V$SESSION WHERE ID<>SESSION_ID();:
   ```

### Step 2: Set Admin Mode

Change the Active server to administrator mode to prevent other transactions from entering.

```sql
ALTER SYSTEM SET ADMIN_MODE = 1;
```

### Step 3: Stop Replication

1. Resolve the replication gap on the Active server.

   ~~~sql
   ALTER REPLICATION replication_name FLUSH;
   ~~~

2. Verify that the replication gap has been resolved. The value of REP_GAP should be 0.

   ~~~sql
   SELECT REP_NAME, REP_GAP FROM V$REPGAP;
   ~~~

3. Stop Replication.

   ~~~sql
   ALTER REPLICATION replication_name STOP;
   ~~~

### Step 4: Remove Replication Target

Remove the DDL statement execution target from all replication objects on the replication servers. 

```sql
ALTER REPLICATION replication_name 
DROP TABLE FROM user_name.table_name TO user_name.table_name;
```

### Step 5: Execute DDL Statement

Execute the DDL statement on all replication servers.

### Step 6: Add Replication Target

Re-add the DDL statement execution target to the replication objects on all replication servers.

```sql
ALTER REPLICATION replication_name
ADD TABLE FROM user_name.table_name TO `user_name.table_name;
```

### Step 7: Start Replication

Start replication on the Active server.

~~~sql
ALTER REPLICATION replication_name START;
~~~

### Step 8: Remove Admin Mode

Remove administrator mode on the Active server.

```sql
ALTER SYSTEM SET ADMIN_MODE = 0;
```

### Step 9: Start Service

Restart the service on the Active server.

### Active-Standby Environment Execution Procedure

<table border="1" cellpadding="5" cellspacing="0">
	<thead>
    	<tr>
      		<th colspan="2">Step</th>
      		<th>Active</th>
      		<th>Standby</th>
    	</tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="2">Step 1. Stop Service</td>
      		<td>Stop Service</td>            
      		<td>Stop Service</td>
      		<td>-</td>
    	</tr>
        <tr>
      		<td>Session Check</td>
      		<td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
      		<td></td>
    	</tr>
        <tr>
      		<td colspan="2">Step 2. Set Admin Mode</td>
      		<td>ALTER SYSTEM SET ADMIN_MODE = 1;</td>
      		<td></td>
    	</tr>
        <tr>
      		<td rowspan="3">Step 3. Stop Replication</td>            
      		<td>Resolve Replication Gap</td>
      		<td>ALTER REPLICATION replication_name FLUSH;</td>
      		<td></td>
    	</tr>
        <tr>
      		<td>Verify the replication gap resolution</td>
      		<td>SELECT REP_NAME, REP_GAP FROM V$REPGAP;</td>
      		<td></td>
    	</tr>                          
        <tr>
            <td>Stop Replication</td>
      		<td>ALTER REPLICATION replication_name STOP;</td>
            <td></td>
    	</tr>
        <tr>
            <td colspan="2">Step 4. Remove Replication Target</td>
      		<td>ALTER REPLICATION replication_name DROP TABLE FROM user_name.table_name TO user_name.table_name;</td>
      		<td>ALTER REPLICATION replication_name DROP TABLE FROM user_name.table_name TO user_name.table_name;</td>
    	</tr>
        <tr>
            <td colspan="2">Step 5. Execute DDL Statement</td>
      		<td>Execute DDL Statement</td>
            <td>Execute DDL Statement</td>
    	</tr>
        <tr>
            <td colspan="2">Step 6. Add Replication Target</td>
      		<td>ALTER REPLICATION replication_name ADD TABLE FROM user_name.table_name TO user_name.table_name;</td>
			<td>ALTER REPLICATION replication_name ADD TABLE FROM user_name.table_name TO user_name.table_name;</td>
    	</tr>
        <tr>
            <td colspan="2">Step 7. Start Replication</td>
      		<td>ALTER REPLICATION replication_name START;</td>
            <td></td>
    	</tr>
        <tr>
      		<td colspan="2">Step 8. Remove Admin Mode</td>
      		<td>ALTER SYSTEM SET ADMIN_MODE = 0;</td>
            <td></td>
    	</tr>
        <tr>
            <td colspan="2">Step 9. Start Service</td>
      		<td>Start Service</td>
            <td>-</td>
    	</tr>                   
	</tbody>
</table>





### Active-Active Environment Execution Procedure

<table border="1" cellpadding="5" cellspacing="0">
	<thead>
    	<tr>
      		<th colspan="2">Step</th>
      		<th>Active1</th>
      		<th>Active2</th>
    	</tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="2">Step 1. Stop Service</td>
      		<td>Stop Service</td>
      		<td>Stop Service</td>
      		<td>Stop Service</td>
    	</tr>
        <tr>
      		<td>Session Check</td>
      		<td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
      		<td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
    	</tr>
        <tr>
      		<td colspan="2">Step 2. Set Admin Mode</td>
      		<td>ALTER SYSTEM SET ADMIN_MODE = 1;</td>
      		<td>ALTER SYSTEM SET ADMIN_MODE = 1;</td>
    	</tr>
        <tr>
            <td rowspan="3">Step 3. Stop Replication</td>            
      		<td>Resolve Replication Gap</td>
      		<td>ALTER REPLICATION replication_name FLUSH;</td>
      		<td>ALTER REPLICATION replication_name FLUSH;</td>
    	</tr>
        <tr>
      		<td>Verify the replication gap resolution</td>
      		<td>SELECT REP_NAME, REP_GAP FROM V$REPGAP;</td>
      		<td>SELECT REP_NAME, REP_GAP FROM V$REPGAP;</td>
    	</tr>     
        <tr>
            <td>Stop Replication</td>
      		<td>ALTER REPLICATION replication_name STOP;</td>
            <td>ALTER REPLICATION replication_name STOP;</td>
    	</tr>
        <tr>
            <td colspan="2">Step 4. Remove Replication Target</td>
      		<td>ALTER REPLICATION replication_name DROP TABLE FROM user_name.table_name TO user_name.table_name;</td>
      		<td>ALTER REPLICATION replication_name DROP TABLE FROM user_name.table_name TO user_name.table_name;</td>
    	</tr>
        <tr>
            <td colspan="2">Step 5. Execute DDL Statement</td>
      		<td>Execute DDL Statement</td>
            <td>Execute DDL Statement</td>
    	</tr>
        <tr>
            <td colspan="2">Step 6. Add Replication Target</td>
      		<td>	ALTER REPLICATION replication_name ADD TABLE FROM user_name.table_name TO user_name.table_name;</td>
			<td>	ALTER REPLICATION replication_name ADD TABLE FROM user_name.table_name TO user_name.table_name;</td>
    	</tr>
        <tr>
            <td colspan="2">Step 7. Start Replication</td>
      		<td>ALTER REPLICATION replication_name START;</td>
            <td>ALTER REPLICATION replication_name START;</td>
    	</tr>
        <tr>
            <td colspan="2">Step 8. Remove Admin Mode</td>
      		<td>ALTER SYSTEM SET ADMIN_MODE = 0;</td>
            <td>ALTER SYSTEM SET ADMIN_MODE = 0;</td>
    	</tr>
        <tr>
            <td colspan="2">Step 9. Start Service</td>
      		<td>Start Service</td>
            <td>Start Service</td>
    	</tr>                   
	</tbody>
</table>





## Environment Where Service Cannot Be Stopped

In environments where the operation of replication servers cannot be stopped simultaneously, DDL statements must be executed sequentially on each server, and [SQL Apply Mode](#appendix-c-sql-apply-mode) must be used.

> ##### Cautions
>
> In this procedure, there is a possibility that some data may not be transmitted at certain points in time. Therefore, it is recommended to choose the time with the least transaction activity for performing the operation. Additionally, before the service migration point, it is advised to temporarily stop the service until the replication gap reaches 0.

### Step 1: Service Migration 

Migrate the service from Active1 to Active2.

1. Resolve the replication gap on Active1.

   ~~~sql
   ALTER REPLICATION replication_name FLUSH;
   ~~~

2. Verify that the replication gap is resolved by checking that the REP_GAP value is 0.

   ~~~sql
   SELECT REP_NAME, REP_GAP FROM V$REPGAP;
   ~~~

3. Migrate the service to Active2.

4. Check the database session to verify that the service has been successfully migrated to Active2.

   ```sql
   SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();
   ```

### Step 2: Set Admin Mode

Change Active1 to administrator mode to prevent new transactions from entering.

~~~sql
ALTER SYSTEM SET ADMIN_MODE = 1;
~~~


### Step 3: Stop Replication

Stop replication on all servers.

~~~sql
ALTER REPLICATION replication_name STOP;
~~~

### Step 4: Remove Replication Target

Remove the DDL Statement execution target on Active1.

```sql
ALTER REPLICATION replication_name
DROP TABLE FROM user_name.table_name TO user_name.table_name;
```

### Step 5: Execute DDL Statement

Execute DDL Statement on Active1

### Step 6: Add Replication Target

Re-add the DDL Statement execution target to the replication object on Active1.

```sql
ALTER REPLICATION replication_name
ADD TABLE FROM user_name.table_name TO user_name.table_name;
```

### Step 7: Enable SQL Apply Mode

Enable SQL Apply Mode on all replication servers.

~~~sql
ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;
~~~

### Step 8: Start Replication

Restart replication on all servers.

```sql
ALTER REPLICATION replication_name START;
```

### Step 9: Remove Admin Mode

Remove administrator mode from Active1.

```sql
ALTER SYSTEM SET ADMIN_MODE = 0;
```

### Step 10: Perform DDL Statement on Active2

Repeat **Steps 1 through 9** on Active2.

```sql
ALTER REPLICATION replication_name START;
```

### Step 11: Verify SQL Apply Mode Operation

Verify that SQL Apply Mode is working correctly across all replication objects. If the DDL statement was successfully executed on the replication target server, there should be no replication objects still operating in SQL Apply Mode.

Execute the following query to confirm that the SQL_APPLY_TABLE_COUNT is 0:

~~~sql
SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;
~~~

### Step 12: Disable SQL Apply Mode

~~~sql
ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;
~~~

### Step 13: Service Distribution

Redistribute the services on Active1 and Active2 back to their original configuration.

### Active-Active Environment Execution Procedure

<table border="1" cellpadding="5" cellspacing="0">
	<thead>
    	<tr>
      		<th colspan="2">Step</th>
      		<th>Active1</th>
      		<th>Active2</th>         
    	</tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="4">Migrate the Service from Active1</td>
      		<td>Resolve Replication Gap</td>
      		<td>ALTER REPLICATION replication_name FLUSH;</td>
      		<td></td>
    	</tr>
        <tr>
      		<td>Verify the replication gap resolution</td>
      		<td>SELECT REP_NAME, REP_GAP FROM V$REPGAP;</td>
      		<td></td>
    	</tr>
        <tr>
      		<td>Service Migration</td>
      		<td>Migrate the service from Active1 to Active2.</td>
      		<td></td>          
    	</tr>
        <tr>
      		<td>Verify Service Migration</td>
      		<td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
      		<td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
    	</tr>
        <tr>
      		<td colspan="2">Set Admin Mode</td>
      		<td>ALTER SYSTEM SET ADMIN_MODE = 1;</td>
      		<td></td>
    	</tr>
        <tr>
      		<td colspan="2">Stop Replication</td>
      		<td>ALTER REPLICATION replication_name STOP;</td>
      		<td>ALTER REPLICATION replication_name STOP;</td>
    	</tr>
        <tr>
            <td colspan="2">Remove Replication Target</td>
      		<td>ALTER REPLICATION replication_name DROP TABLE FROM user_name.table_name TO user_name.table_name;</td>
      		<td></td>
    	</tr>        
        <tr>
            <td colspan="2">Execute DDL Statement</td>
      		<td>Execute DDL Statement</td>
            <td></td>
    	</tr>
        <tr>
            <td colspan="2">Add Replication Target</td>
      		<td>ALTER REPLICATION replication_name ADD TABLE FROM user_name.table_name TO user_name.table_name;</td>
			<td></td>
    	</tr>
        <tr>
      		<td colspan="2">Enable SQL Apply Mode</td>
      		<td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
      		<td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;</td>
    	</tr>         
        <tr>
            <td colspan="2">Start Replication</td>
      		<td>ALTER REPLICATION replication_name START;</td>
            <td>ALTER REPLICATION replication_name START;</td>
    	</tr>
        <tr>
      		<td colspan="2">Remove Admin Mode</td>
      		<td>ALTER SYSTEM SET ADMIN_MODE = 0;</td>
            <td></td>
    	</tr>        
        <tr>
            <td rowspan="4">Migrate the Service from Active2</td>
      		<td>Resolve Replication Gap</td>
      		<td></td>
            <td>ALTER REPLICATION replication_name FLUSH;</td>
    	</tr>
        <tr>
      		<td>Verify the replication gap resolution</td>
      		<td></td>
      		<td>SELECT REP_NAME, REP_GAP FROM V$REPGAP;</td>      
    	</tr>
        <tr>
      		<td>Migrate service</td>
      		<td></td>
      		<td>Migrate the service from Active1 to Active2.</td>
    	</tr>
        <tr>
      		<td>Verify Service Migration</td>
      		<td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>
      		<td>SELECT COUNT(*) FROM V$SESSION WHERE ID <> SESSION_ID();</td>         
    	</tr>       
        <tr>
      		<td colspan="2">Set Admin Mode</td>
      		<td></td>
      		<td>ALTER SYSTEM SET ADMIN_MODE = 1;</td>
    	</tr>
        <tr>
      		<td colspan="2">Stop Replication</td>
      		<td>ALTER REPLICATION replication_name STOP;</td>
      		<td>ALTER REPLICATION replication_name STOP;</td>
    	</tr>
        <tr>
            <td colspan="2">Remove Replication Target</td>
      		<td></td>
      		<td>ALTER REPLICATION replication_name DROP TABLE FROM user_name.table_name TO user_name.table_name;</td>
    	</tr>        
        <tr>
            <td colspan="2">Execute DDL Statement</td>
      		<td></td>
            <td>Execute DDL Statement</td>
    	</tr>
        <tr>
            <td colspan="2">Add Replication Target</td>
      		<td></td>
			<td>ALTER REPLICATION replication_name ADD TABLE FROM user_name.table_name TO user_name.table_name;</td>
    	</tr> 
        <tr>
            <td colspan="2">Start Replication</td>
      		<td>ALTER REPLICATION replication_name START;</td>
            <td>ALTER REPLICATION replication_name START;</td>
    	</tr>        
        <tr>
            <td colspan="2">Verify SQL Apply Mode Operation</td>
      		<td>SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;</td>
            <td>SELECT REP_NAME, SQL_APPLY_TABLE_COUNT FROM V$REPRECEIVER;</td>          
    	</tr>
        <tr>
            <td colspan="2">Disable SQL Apply Mode</td>
      		<td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
            <td>ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 0;</td>
    	</tr>        
        <tr>
      		<td colspan="2">Remove Admin Mode</td>
      		<td></td>
            <td>ALTER SYSTEM SET ADMIN_MODE = 0;</td>
    	</tr> 
    	<tr>
  			<td colspan="2">Service Distribution</td>
  			<td>Redistribute the service back to its original configuration
        </td>
        	<td></td>
		</tr>                  
	</tbody>
</table>







# Appendix C: SQL Apply Mode

## Overview

SQL Apply Mode is used to maintain replication when **metadata between the local and remote servers differs**. When enabled, XLogs are converted into SQL statements to replicate the primary transaction. This feature is necessary in various situations where DDL statements are executed on replication targets.

### Restrictions

- EAGER mode replication is not supported.
- It does not work on replication target tables with encrypted columns.

### Cautions

Enabling SQL Apply Mode significantly slows down replication, so it **should be disabled immediately after use**.

## Conditions for SQL Apply Mode Operation

SQL Apply Mode operates in the following situations:

#### Column Information Mismatch

- Data types are different.

- Data types are the same, but size, precision, or scale differ.


#### Constraint Mismatch

- The condition of a CHECK constraint differs.

- The name of a CHECK constraint differs.

- The NOT NULL / NULL constraint on a column differs.

#### Index Information Mismatch

- The configuration of a unique key index differs.

- The unique key index includes non-replication target columns.

- The configuration of a function-based index differs.

- The function-based index includes non-replication target columns.

#### Partition Information Mismatch

- The number of partitions in the replication pair differs.

## Setting the SQL Apply Mode

SQL Apply Mode is set on the **replication receiver** side.

#### How to Set the SQL Apply Mode

To enable SQL Apply Mode on the receiver server, execute the following statement:

```sql
ALTER SYSTEM SET REPLICATION_SQL_APPLY_ENABLE = 1;
```

#### Setting Verification Method

To verify if the setting has been applied correctly, execute the following query on the receiver server:

```sql
SELECT NAME, VALUE1 FROM V$PROPERTY WHERE NAME = 'REPLICATION_SQL_APPLY_ENABLE';
```

Example Result:

~~~sql
NAME                            VALUE1                          
-------------------------------------------------------------------
REPLICATION_SQL_APPLY_ENABLE    1                               
1 row selected.
~~~

If the value of `VALUE1` is 1, it indicates that SQL Apply Mode has been successfully activated.
