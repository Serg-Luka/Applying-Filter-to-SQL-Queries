# Applying Filters to SQL Queries

## Objective

In this lab, I applied additional filters to SQL queries to extract specific information from a database. I utilised standard SQL operators to filter data based on particular dates and times. Throughout the process, I executed SQL queries using the MariaDB shell. This is a QuickLabs-based project hosted on the Google Cloud platform.

### Skills Acquired

- Writing SQL queries to retrieve data from databases.
- Using various operators to filter records based on specific conditions.
- Combining multiple conditions in SQL queries to refine search results.
- Interacting with the MariaDB shell and reconnecting to the database if the session is unintentionally closed.

### Tools and Environment Used

- MariaDB
- Linux

## Scenario

In this project, I am investigating a recent security incident.

I need to gather information about login attempts from certain dates and times to assist in resolving the issue.

The steps include retrieving login events after a specific date, narrowing the search to a date range, investigating logins at particular times, and finally filtering login attempts based on event IDs.

## My Procedure

**I divided the procedure into four main tasks, as detailed below:**

### Task 1: Retrieve Login Attempts After a Certain Date

In this task, I am investigating a recent security incident and need to collect information about login attempts made after a specific date.

I carried out this task in two steps:

1. To retrieve data for login attempts made after '2022-05-09', I completed the SQL query using the greater-than operator:

```
SELECT * FROM login_attempts WHERE login_time > '2022-05-09';
```


![Z1](https://github.com/godfreyndlovu/Applying-filters-to-SQL-queries/assets/102636518/62bc2f7d-ac0b-4026-b449-8d046554548e)

The number of login attempts made after '2022-05-09' is **125**.

2. Based on my initial query, I expanded the date range to include login attempts made on or after '2022-05-09'. To do this, I used the greater-than-or-equal-to operator:

```
SELECT * FROM login_attempts WHERE login_time >= '2022-05-09';
```


![Z2](https://github.com/godfreyndlovu/Applying-filters-to-SQL-queries/assets/102636518/8c28d358-5216-49c0-80b3-526b26d10b86)

The number of login attempts made from '2022-05-09' onward is **165**.

### Task 2: Retrieve Login Attempts Within a Date Range

In this task, I needed to narrow the scope of my search and exclude login attempts made after '2022-05-11'. 

To achieve this, I used the BETWEEN and AND operators to filter results between '2022-05-09' and '2022-05-11':

```
SELECT * FROM login_attempts WHERE login_time BETWEEN '2022-05-09' AND '2022-05-11';
```


![Z3](https://github.com/godfreyndlovu/Applying-filters-to-SQL-queries/assets/102636518/a5566657-c170-4c30-8f99-f2b184ef4a65)

There were **123** login attempts made between '2022-05-09' and '2022-05-11'.

### Task 3: Investigate Logins at Specific Times

In this task, I needed to investigate logins that occurred at specific times. To begin, I needed to filter the data in the `login_attempts` table by the `login_time` field.

Our organisation's typical working hours begin at 07:00:00, so I aimed to retrieve all login attempts made before 07:00:00 to examine users logging in outside of standard hours.

1. I wrote an SQL query to retrieve data for login attempts made before '07:00:00':

```
SELECT * FROM login_attempts WHERE TIME(login_time) < '07:00:00';
```


![Z4](https://github.com/godfreyndlovu/Applying-filters-to-SQL-queries/assets/102636518/8175fd85-f794-483b-8574-722483d23bc0)

The username in the fifth record returned by this query is **eraab**.

2. The query in the previous step returned more results than needed. I modified the query to return logins between '06:00:00' and '07:00:00':

```
SELECT * FROM login_attempts WHERE TIME(login_time) BETWEEN '06:00:00' AND '07:00:00';
```


This query selects all rows from the `login_attempts` table where the time component of `login_time` falls between 06:00:00 and 07:00:00.

![Z5](https://github.com/godfreyndlovu/Applying-filters-to-SQL-queries/assets/102636518/0b40e9d8-6043-4673-aa9d-f39ef96363e6)

The earliest login attempt was at **06:01:31**.

### Task 4: Investigate Logins by Event ID

In the final task, I needed to investigate login attempts based on event ID numbers. For this query, I aimed to retrieve only the `event_id`, `username`, and `login_date` fields from the `login_attempts` table.

1. To filter login attempts with `event_id` greater than or equal to 100, I wrote the following query:

```
SELECT * FROM login_attempts WHERE event_id >= 100;
```


![Z6](https://github.com/godfreyndlovu/Applying-filters-to-SQL-queries/assets/102636518/fff842bd-980e-4a4f-8943-4837e1e4105c)

The login date of the third result returned is **2022-05-09**.

2. The previous query returned more data than required. I modified the query to filter only login attempts with `event_id` between 100 and 150:

```
SELECT * FROM login_attempts WHERE event_id BETWEEN 100 AND 150;
```


This query selects all columns (`*`) from the `login_attempts` table where the `event_id` falls between 100 and 150, inclusive.

![Z7](https://github.com/godfreyndlovu/Applying-filters-to-SQL-queries/assets/102636518/8ab8268c-b14e-4cfb-adee-d4976c7e9de4)

The username of the seventh result is **tmitchel**.

## Conclusion

The goal of this project was to apply SQL querying skills to investigate a recent security incident by filtering and analysing login data stored in a MariaDB database. The tasks involved retrieving specific records based on date, time, and event ID criteria, using a variety of SQL operators and functions. By completing these tasks, I demonstrated my ability to filter data, handle dates and times, perform range queries, and manage real-world data, which are all essential skills for a cybersecurity analyst.
