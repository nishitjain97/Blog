---
title: 1. Introduction to Advanced Java
description: Java language advanced features
toc: true
authors:
tags:
categories:
series:
date: '2020-09-01'
lastmod: '2020-09-01'
---

## Introduction

- For web applications

- Technologies are

    - JDBC (for DB connection)

    - Servlets (For background processing)

    - JSPs (Presentation or user view)

## JDBC

- Part of Java Standard Edition

- It is a specification (guideline) defined by Java vendor and implemented by database vendors

- Implementation is called driver

- Features:

    - Standard API: database independent

    - Platform independent

    - CRUD (Create or insert, Retrieve (select), Update, Delete)

    - Large support for JDBC

### JDBC Architecture

<div>
    <img src="/docs/java/advanced_java_ocjp_scjp/jdbc_flowchart.png" style="height:300px;margin:auto;">
</div>

- JDBC API provides driver manager to Java applications

- Application can communicate with any DB using driver manager and DB specific driver software

- Driver manager

    - A class present inside java.sql package

    - Manages all DB drivers

    - Registers and unregisters drivers

        ```
        DriverManager.registerDriver(driver)
        DriverManager.unregisterDriver(driver)
        ```

    - Establishes connection with DB using driver software

        ```
        Connection con = DriverManager.getConnection(jdbcUrl, username, password)
        ```

- DB drivers

    - Bridge between java app and database

    - Converts java calls to DB specific calls and vice versa

## JDBC API

- Provides classes and interfaces for programmers to communicate with databases and driver software vendors to develop driver softwares

- Contains 2 packages

    - java.sql package: Basic classes and interfaces for DB connunication

        - Interfaces: Driver, Connection, Statement, PreparedStatement, CallableStatement, ResultSet

        - Classes: DriverManager, Date, Time, TimeStamp, Types

    - javax.sql package: 
    
        - Advanced classes and interfaces for DB communications

        - Contains multiple sub-packages

            - javax.sql.rowset

            - javax.sql.rowset.serial

            - javax.sql.rowset.spi

        - Interfaces: DataSource (used for connection pooling concept), RowSet, RowSetListener, ConnectionEvenListener

        - Classes: RowSetEvent, ConnectionEvent

- Driver software is a group of implementation classes of JDBC API, made by driver vendors

- Driver(I) is present in java.sql and provides specification to implementation classes

- **Note:** jar (java archive files) is a group of .class files

- Driver software is in the form of jar file

    - Java vendor -> Type1 driver

    - DB vendor -> Type2 driver

    - 3rd party vendor -> Inet -> E.g. Inet Oraxo for Oracle

- **Note:** DB vendor driver software is highly recommended

###  Types of drivers

- Type 1 driver: JDBC-ODBC bridge driver or bridge driver

- Type 2 driver: Native API-partly Java driver or native driver

- Type 3 driver: All java net protocol driver or network protocol driver or middleware driver

- Type 4 driver: All Java Native protocol driver or pure driver or thin driver

#### Type 1 driver

<div>
    <img src="/docs/java/advanced_java_ocjp_scjp/type_1_driver.png" style="height:150px;margin:auto;">
</div>

- Converts Java calls to ODBC calss (uses support of ODBC drivers)

- Comes with Java SDK (made by vendor)

- DB independent driver

- Slow because two conversions are required

- Platform dependent because ODBC is available only for Windows machines

- Supported only till version 1.7

#### Type 2 driver

<div>
    <img src="/docs/java/advanced_java_ocjp_scjp/type_2_driver.png" style="height:150px;margin:auto;">
</div>

- Faster than type 1 (vendor provided library calls are understandable by DB)

- No ODBC, so more portable than type 1

- DB and platform dependent

- Native libraries might not be present

- 