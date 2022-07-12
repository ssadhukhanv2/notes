## SQL


* [Full **LeetCode SQL**](https://leetcode.com/list/e55d9ob1/)

* [Find **Second highest salary**-> ``order by e.salary desc offset 1 rows fetch next 1 rows only``](https://leetcode.com/problems/second-highest-salary/)

        --inner query
        select max(salary)"SecondHighestSalary" from employee e where e.salary<(select max(e1.salary) from employee e1);

        --offset and fetch next
        select salary "SecondHighestSalary" from employee e order by e.salary desc offset 1 rows fetch next 1 rows only;


* [Find **N th highest salary**-> **``dense_rank()``** ``OVER(ORDER BY E.SALARY DESC)``](https://leetcode.com/problems/nth-highest-salary/)

        SELECT EMP.SALARY INTO result FROM (SELECT E.ID,E.SALARY,DENSE_RANK() OVER(ORDER BY E.SALARY DESC) "DENSE"  FROM EMPLOYEE E) EMP
            WHERE  EMP.DENSE=N;

* [What is the difference between **``rank(), dense_rank()``** and **``row_num()``**](https://javarevisited.blogspot.com/2016/07/difference-between-rownumber-rank-and-denserank-sql-server.html#axzz7UR2Yz9T0)
* [Two tables are there Person & Address, return all person along with their corresponding addresses, return null if a person does not have entries in the address table **``left Join``**](https://leetcode.com/problems/combine-two-tables/submissions/)
* [Two tables Customers and Orders. Find Customers who never orders **``not exists``**(preferable) or **``not in``**](https://leetcode.com/problems/customers-who-never-order/)

        select name "Customers" from customers c where not exists (select customerid from orders o where o.customerid=c.id);
* [Find second highest of salary from the employee table **``not in``** or **``limit offset desc``**(check later)](https://leetcode.com/problems/second-highest-salary/submissions/)
* [How will you use **``limit and offset``**](https://www.oracletutorial.com/oracle-basics/oracle-fetch/#:~:text=The%20OFFSET%20clause%20specifies%20the,that%20evaluates%20to%20a%20number.)
* [Find all **duplicate emails** in a table](https://leetcode.com/problems/duplicate-emails/)

        select email from person group by email having count(*)>1;
* [Find rising temperature **connect by prior**](https://leetcode.com/problems/rising-temperature/discuss/2043679/Oracle)
* [What is the difference betweeen **where**(can't have aggregate functions, executed after from, before group by) and **having**(can have aggregate functions, executed after group by)](https://www.youtube.com/watch?v=L-URbfgxBMQ)


* [SQL Interview Questions](https://towardsdatascience.com/5-common-sql-problems-for-you-to-crush-10a796258643)


## 
* [Explain **Views**]
* [What is a **cursor**]




## Joins
* Suppose there are two tables **pallete_a(id,color)** & **pallete_a(id,color)**
* [Find **colors that exists on both table** -> **inner join** on color attributes](https://www.oracletutorial.com/oracle-basics/oracle-joins/)
* [Find **colors unique to pallete_A**(colors that exist in pallete_A that don't exits in pallete_B) -> **left outer join** on color **with additional condition**](https://www.oracletutorial.com/oracle-basics/oracle-joins/)
* [Find **colors unique to pallete_B**(color that don't exist in pallete_A exist in pallete_B)-> **right outer join**  on color **with additional condition**](https://www.oracletutorial.com/oracle-basics/oracle-joins/)
* [Find the **unique colors of both palletes**->**full outer join** with **additional condition**](https://www.oracletutorial.com/oracle-basics/oracle-joins/)


## Oracle 
* [What is the **difference** between **varchar**(holds upto 2000 bytes, holds space for characters) and **varchar2**(Stores upto 4000 bytes, releases unused space)](https://youtu.be/40VYT0cMHSs?t=171)
* [What are the **components of logical database structure** in Oracle -> **Tablespace** (Logical Storage Unit where the Database Schema Objects are stored) and **Schema**(Collection of Database objects Owned by an User)](https://youtu.be/40VYT0cMHSs)
* [What is a table in Oracle](https://youtu.be/40VYT0cMHSs?t=269)
* [Relationship between **database**(contains multiple tablespaces), **tablespace**(Logical Storage Units in the Oracle database) and **datafiles**(Each oracle database consists of one or more datafiles. Physical files that confirms with the OS)](https://youtu.be/40VYT0cMHSs?t=319)
* [Various database objects in Oracle **Tables, Tablespaces, Views, Indexes, Synonyms**](https://youtu.be/40VYT0cMHSs?t=388)
* [Explain **analyze**(collect or delete statistics about a database object) command in oracle](https://youtu.be/40VYT0cMHSs?t=423)