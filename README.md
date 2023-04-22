## SQL

Database: A container to store organized data

What can we do with SQL in daily work?

1. Accessing and manipulating databases
2. Create reports via Excel, Power BI, Tableau, Paginated Reports
3. Perform data analytics and provide business insights
4. Process automation
5. And more...

### *Column Name / Header* - Naming Standards:

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

### Data Type

1. *Numeric data*
   * **`int`** - integer -> no decimals i.e. quantity, age
   * **`float`** - floating-point number -> with decimals, 32 bit in size i.e. salary, price
   * **`double`** - double-precision floating-point number -> with decimals, double the precision than float (64 bit in size)
2. *Date and time*
   * **`date` - YYYY-MM-DD**
   * **`time` (time point or range) - HH:MM:SS**
   * **`datetime` - YYYY-MM-DD HH:MM:SS**
3. *String (text format i.e. name, id, memo, notes)*
   * **`char`**-> save up to 255bytes, fixed in length
     * i.e. char(10) will always occupy 10bytes even if only used 2bytes
     * used in i.e. fixed-lenth & combination id or titles
   * **`varchar`** -> save up to 65,535bytes, vary in length
     * i.e. varchar(10) takes max 10 bytes; if only used 2bytes then it occupies 2bytes
     * used in i.e. names, notes

### Table/column manipulations

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

### Fact table & Reference/Dimension table

* Fact table: measurements, metrics, and facts about a business process
* Reference/Dimension table: contains descriptive attributes to be used as query constraining

### Constraints

Rules given how database data is inserted or manipulated

1. NOT NULL CONSTRAINT

   - Blank(NULL) vs Empty: Null refers as nothing (often shown as <*null*>); empty refers to an unique string with 0 length
   - 'NULL' is considered as a str
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

### Retrieving and Filtering Data

1. Retrieving Data: `SELECT`

   1. Retrieving multiple columns

      ```
      SELECT column_1, column_2, column_3
      FROM table_name
      ```

      If this table has 4 columns, it will only retrieve 3 with corresponding names
   2. Retrieving all columns:

      ```
      SELECT *
      FROM table_name
      ```

      Not recommended to use since tables might have large amount of data. Retrieving all of them could cause issues to server

      May be used when not familiar with the table, could be used with `LIMIT`:

      ```
      SELECT * FROM table_name
      LIMIT 100 /*this will only return the first 100 default-ordered rows*/
      ```

      ***Only select the data/columns/rows needed***

      Amount of data selected will also affect the server runtime
   3. Retrieving distinct rows - return unique values

      ```
      SELECT distinct column_1, column_2, column_3
      FROM table_name
      ```
2. Filtering Data: `WHERE`

   ```
   SELECT column_1, column_2, column_3
   FROM table_name
   WHERE condition  /*condition: specified condition for the selected column to satisfy it*/
   ```

   `WHERE` Clause Operators:

   1. `=`: Equality (str, num, date), usually used for str
   2. `<> / !=`: Not-equality (str, num, date)
   3. `< / <= / !<`: Less than / less than or equal to / no less than (num. date)
   4. `> / >= / !>`: Greater than / greater than or equal to / no greater than (num, date)
   5. `BETWEEN value1 and value2`: Between two specific values (inclusive range) (num, date)
   6. `IS NULL / IS NOT NULL`: Is a NULL value / is not a NULL value

### Date and Time Related Questions

Get current date and time:

```
SELECT now() #MySQL
SELECT getdate() #SQL Server
```

My SQL - `timestampdiff(unit, datetime_expr1, datetime_expr2)`

* Calculated based on date
* `date_add()`: calculated based on unit (e.g. year or month)
* e.g.
  ```
  select * from employees
  where timestampdiff(year, hrie_date, now()) <= 30

  select * from employees
  where hire_date > date_add(now(), interval -31 years)
  ```

When datatype is DATETIME, usually use `< / >` instead of `<= / >=` since default time is 00:00:00

* e.g. select call records before 2023-01-31, including 2023-01-31:

  ```
  👍call_dttm < '2023-02-01'
  👎call_dttm <= '2023-01-31' #Missing records on 01-31
  ```

### Logic Keywords

Usually used in condition clause (where, having, case when)

1. `BETWEEN` (num, date, datetime, calculable variables)

   ```
   SELECT column_1, column_2, column_3
   FROM table_name
   WHERE column_1 BETWEEN value_1 and value_2
   ```

   - Value_1 and value_2 are the begin and end values of the range
   - `BETWEEN` operator is inclusive: begin and end values are included - [value_1, value_2]
   - Begin and end values are variables that can be calculated
     - e.g. num, date, dttm, amount, qty, salary, etc.
2. `NOT BETWEEN` (num, date)

   ```
   SELECT column_1, column_2, column_3
   FROM table_name
   WHERE column_1 NOT BETWEEN value_1 and value_2
   ```

   - Value_1 and value_2 are the upper and lower bounds of the range
   - `NOT BETWEEN` is not inclusive: upper and lower bound values are not included
3. `IN` (str)

   ```
   SELECT column_1, column_2, column_3
   FROM table_name
   WHERE column_1 IN (value_1, value_2)
   ```

   - Test whether the values in column_1 match value_1 or value_2
   - Value_1 and value_2 are usually categorical variables
     - e.g. str, order_type, contract_type, region, region_managers, measures, dept_no
4. `NOT IN` (str)

   ```
   SELECT column_1, column_2, column_3
   FROM table_name
   WHERE column_1 NOT IN (value_1, value_2)
   ```

   - Opposite of `IN`, return values in column_1 that do not match either value_1 or value_2
5. `NOT IN` and `NULL / IFNULL`

   - `NOT IN`:

     ```
     select * from table_name
     where column_1 not in (value_1)
     ```

     Expected to return values that are not value_1, but if the value is NULL/blank (*< null >*), it would not be returned
   - `IFNULL` (MySQL):

     ```
     IFNULL(column_1, 'return_value')
     ```

     If column_1 is NULL, return return_value
   - Combining both:

     ```
     select * from table_name
     where IFNULL(column_1, '') not in (value_1)
     ```

     This will return all values, including NULL, that are not value_1
6. `AND` and `OR` / `UNION` and `UNION ALL`

   - `AND` is used when multiple conditions are all satisfied, used in e.g. where or case when

     ```
     select * from table_name
     where condition_1 AND condition_2 AND condition_3
     ```

     Usually each condition will be a different variable
   - `OR` is used when any one of the listed conditions is satisfied, used in e.g. where or case when

     ```
     select * from table_name
     where condition_1 OR condition_2 OR condition_3
     ```

     Each condition can be the same variable or a combination of diff variables, can be used to replace `IN`
   - `AND` has higher priority than `OR` in SQL - `AND` will be executed first if not otherwise specified
   - `UNION` and `UNION ALL` is used to combine multiple columns/tables with similar format/datatype/order and return a result table

     - `UNION` will exclude the duplicated data, only display distinct data
     - `UNION ALL` will include all selected data from the tables
7. `LIKE` (str)

   ```
   SELECT column_1, column_2, column_3 FROM table_name
   WHERE column_1 LIKE '%TEXT%'
   ```

   `LIKE '%A'`: return data that end with 'A' e.g. 'vvBETA'

   `LIKE 'B%'`: return data that start with 'B' e.g. 'BEEabc'

   `LIKE '%LATE%'`: return data that include with 'LATE' in any position e.g. 'BELATED'

   `LIKE 'A%E'`: return data that start with 'A' and end with 'E' e.g. 'APPLE'

   `LIKE '%'`: return all data excluding NULL, similar to `IS NOT NULL`

### Data Sorting (order by)

Default order: 0 to 9, A to Z, ascending order

Usually used on num or date-related data, sometimes str

```
select column_1, column_2, column_3
from table_name
order by column_1 desc
```

Ascending order (asc): by default in SQL

Decending order (desc)

### Data Calculation and Manipulation

1. Data Calculation

   - Separated fields e.g.

     - `'first_name' and 'last_name'`
     - `'address_1', 'address_2', 'city', 'state', and 'zip_code'`
   - Case sensitive data (mixed uppercase and lowercase)
   - Type code e.g.

     Dry Van: DRY01, DRY02

     Heater: HET01, HET02, HET03
   - Mathmatical calculation (calculation field) e.g.

     - sales_price = unit_price * qty
     - hire_years = timestampdiff(year, now(), hire_date)

   `CONCAT`: combine separated fields

   ```
   SELECT CONCAT(column_1, column_2, ' ', ',', column_3) AS column_new
   FROM table_name
   ```

   Can be used in JOIN: uses and / concat, or multiple variables that repeat (e.g. repeat calls)

   Common str conversions:

   - `TRIM()`: removes spaces or other specified characters from both start & end of a str

     `````
     select trim('   SQL tutorial     ') as column_1 => 'SQL tutorial'
     `````
   - `LTRIM()`: removes spaces on the left side of a str

     ```
     select ltrim('   SQL tutorial     ') as column_1 => 'SQL tutorial     '
     ```
   - `RTRIM()`: removes spaces on the right side of a str

     ```
     select rtrim('   SQL tutorial     ') as column_1 => '   SQL tutorial'
     ```
   - `UPPER()`: converts all characters in a str to uppercase

     ```
     select upper('SQL tutorial') as column_1 => 'SQL TUTORIAL'
     ```
   - `LOWER()`: converts all characters in a str to lowercase

     ```
     select lower('SQL tutorial') as column_1 => 'sql tutorial'
     ```
   - `LEFT()`: return the specified num of char from a str, starting from left

     ```
     select left('SQL tutorial', 3) as column_1 => 'SQL'
     ```
   - `RIGHT()`: return the specified num of char from a str, starting from right

     ```
     select right('SQL tutorial', 9) as column_1 => ' tutorial'
     ```
   - `ROUND()`: rounds a num to a specified num of decimal places

     ```
     select round(32.35, 1) as round_num => 32.4
     ```
   - `ABS()`: return the absolute value of a num

     ```
     select abs(-32.35) as abs_num => 32.35
     ```
2. Mathematical Calculations - calculation field (row)

   - Addition `+`
   - Subtraction `-`
   - Multiplication `*`
   - Division `/`
3. Summarizing Data (Aggregate Functions) - result (column)

   Aggreagte Function: functions that operate on a set of rows to calculate and return a single value

   - `AVG()`: returns a column's avg value
   - `COUNT()`: returns the num of rows in a column
   - DISTINCT: not duplicated
   - `MAX()`: returns a column's highest value
   - `MIN()`: returns a column's lowest value
   - `SUM()`: returns the sum of a column's value
     **NULL is ignored by these functions**
4. Grouping Data

   `GROUP BY`: groups rows that have the same values into summary rows e.g. 'get the num of employees in each gender'

   ```
   SELECT gender, count(distinct emp_no) as emp_count
   FROM employees
   GROUP BY gender
   ```

### Filtering Groups (`HAVING`)

`WHERE` clause is followed by a condition (filter the field with e.g. `> / < / =`), cannot be used with aggregate function

`HAVING` is used with aggregate function (e.g. `COUNT, SUM, AVG, etc.`), **usually used with `GROUP BY`**

```
select gender, count(emp_no) as emp_count 
from employees
group by gender
having count(emp_no) > 150000
```

### Grouping and Sorting

SQL statements & clauses order:

```
select column_1, column_2, column_3
from table_1
(1) where condition_1
(2) group by column_1
(3) having condition_2 (aggregate function)
(4) order by column_1
```

### Subqueries

A subquery is a nested query where the results of one query can be ised in another query via a relational operator or aggregation function

* A SQL statement embedded in another statement
* Can occur in: `WHERE, SELECT, FROM, HAVING` clauses (most commonly used in first three)

e.g. Return all employees in dept_emp table that had been to more than one departments:

```
select a.*
from(
      select emp_no, count(distinct dept_no) as dept_count
from dept_emp
group by emp_no) as a
where a.dept_count > 1
```

1. Subqueries in `WHERE` clause

   e.g. Find the data of all current department managers in employees table

   ```
   select * from employees
   select * from dept_manager

   #find all current dept manager:
   select * from dept_manager
   where to_date = '9999-01-01'

   #find the corresponding emp_no in employees table
   select * from employees
   where emp_no in (
                     select emp_no from dept_manager
                     where to_date = '9999-01-01')

   ```
2. Subqueries in `FROM` clause

   e.g. Find the number of employees whose avg salary is > 85k in salaries table

   ```
   #get the avg salaries of each employee from previous years
   select emp_no, avg(salary) as avg_salary 
   from salaries
   group by emp_no

   #get the employees whose avg salary > 85k (similar to a pivot table)
   select emp_no, avg(salary) as avg_salary 
   from salaries
   group by emp_no
   having avg(salary) > 85000

   #use count to get the num of employees
   select (*) as emp_count
   from (
          select emp_no, avg(salary) as avg_salary 
          from salaries
          group by emp_no
          having avg(salary) > 85000) as a
   ```
3. Subqueries in `SELECT` clause

   e.g. Find how many years of salary did each employee get in salaries table

   ```
   select emp_no,
          (select count(*) from salaries
           where salaries.emp_no = employees.emp_no) as salary_years
   from employees
   group by emp_no
