## SQL

Database: A container to store organized data

What can we do with SQL in daily work?

1. Accessing and manipulating databases
2. Create reports via Excel, Power BI, Tableau, Paginated Reports
3. Perform data analytics and provide business insights
4. Process automation
5. And more...

*Column Name / Header* - Naming Standards:

1. name must contain only a to z (normally use lower case), 0 to 9, and underscore (used to connect words instead of spaces)
2. names can contain multiple underscores (no space b/w words)
3. names must not be too generic
4. use plural for table names
5. short form of a word / phrase i.e. department_number > dept_no
   * number > num / no
   * department > dept
   * service > serv
   * contract > contr
   * operations > ops
   * customers > cust
   * date > dt
   * datetime > dttm
   * employee > emp

*Row / Record*

*Column - usually have the same datatype*

Data Type

1. *Numeric data*
   * **int** - integer -> no decimals i.e. quantity, age
   * **float** - floating-point number -> with decimals, 32 bit in size i.e. salary, price
   * **double** - double-precision floating-point number -> with decimals, double the precision than float (64 bit in size)
2. *Date and time*
   * **date - YYYY-MM-DD**
   * **time (time point or range) - HH:MM:SS**
   * **datetime - YYYY-MM-DD HH:MM:SS**
3. *String (text format i.e. name, id, memo, notes)*
   * **char**-> save up to 255bytes, fixed in length
     * i.e. char(10) will always occupy 10bytes even if only used 2bytes
     * used in i.e. fixed-lenth & combination id or titles
   * **varchar** -> save up to 65,535bytes, vary in length
     * i.e. varchar(10) takes max 10 bytes; if only used 2bytes then it occupies 2bytes
     * used in i.e. names, notes

##### Table/column manipulations

1. Basic Table Creation

```
create table table_name
(
column_name1 datatype constraint,  /*constraint is optional, column name and datatype are mandatory for a table*/
column_name2 datatype constraint,
column_name3 datatype constraint
)
```

* char is usually used for any id since id often have fixed length and sometimes characters i.e. char(5) -> d0100
* phone number usually use char to restrict length and for a consistent format, the number itself gives no meaning

2. Deleting Table

```
drop table table_name
```

3. Updating Tables - add a new column

```
alter table table_name
add column column_name datatype constraint
```

4. Updating Tables - remove a column

```
alter table table_name
drop column column_name
```

5. Updating Tables - rename a table

```
alter table table_name
rename to new_table_name
```

6. Insert Data

* Insert a single complete row

  ```
  insert into table_name
  values('value_11', 'value_12', 'value_13', 'value_14', 'value_15'),
        ('value_21', 'value_22', 'value_23', 'value_24', 'value_25')
  ```
* Insert a single partial row

  ```
  insert into table_name (column_11, column_12, column_13)  /*only insert values into these 3 columns*/
  values('value_11', 'value_12', 'value_13')
  ```
* Inserting retrieved data

  ```
  insert into table_name_1 (column_11, column_12, column_13)
  select column_21, column_22, column_23 from table_name_2
  /*insert column data from table_name_2 into columns of table_name_1*/
  ```
* Copying from one table to another

  ```
  create table table_copy as
  select * from table_curr
  ```
* Column modifications

  renaming a column

  ```
  alter table table_name
  rename column column_name to column_newname
  ```

  modify datatype of a column

  ```
  alter table table_name
  modify column column_name new_datatype
  ```

##### Fact table & Reference/Dimension table

Fact table: measurements, metrics, and facts about a business process
Reference/Dimension table: contains descriptive attributes to be used as query constraining

##### Constraints

Rules given how database data is inserted or manipulated

1. NOT NULL CONSTRAINT

   - Blank(NULL) vs Empty: Null refers as nothing (often shown as <*null*>); empty refers to an unique string with 0 length
   - With NOT NULL CONSTRAINT, the content cannot be null, it has to be given a specific data
   - Usually used in ref/dimension table
2. PRIMARY KEY CONSTRAINT

   - Primary key: A primary key is a special constraint used to ensure that values in a column are unique and never change
   - Usually found in ref table; e.g. dept_no in departments table, emp_no in employees table
   - Conditions:
     1. All rows must have distinct and unique primary key value
     2. Every row must have a primary key value > cannot have null primary key value
     3. Columns containing primary key values can never be modified/updated
     4. Primary key values can never be reused
3. UNIQUE CONSTRAINT

   - Content must be unique and distinct, data content is not repetitive but can contain NULL
   - A table can contain multiple unique constraints, but only one primary key is allowed per table
   - Unique constraint columns can contain NULL values
   - Unique constraint columns can be modified/updated
   - Unlike primary keys, unique constraints cannot be used to define foreign keys
4. FOREIGN KEY CONSTRAINT

   - Foreign Key: A foreign key is a column in a table whose values must match values of a column in another table
   - Main function is to connect with primary key
   - Foreign key constraint prevents invalid data from being inserted into the foreign key column, since it has to be one of the values contained in the parent table(ref table)
5. DEFAULT CONSTRAINT

   - Default constraint: insert default value into the column; if there are no other specified values, the default value will be inserted into the new records
   - e.g. sales date usually use dafault values generated

##### Retrieving and Filter Data


##### Date and Time Related Questions
