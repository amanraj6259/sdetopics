
use aman
CREATE TABLE Employee (
    Emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    salary INT,
    manager_id INT
);

INSERT INTO Employee (Emp_id, emp_name, salary, manager_id) VALUES
(1, 'A', 500, NULL),
(2, 'B', 400, 1),
(3, 'C', 700, 1),
(4, 'D', 450, 2),
(5, 'E', 475, 2),
(6, 'F', 475, 2);

select *From Employee e1 inner join Employee emp on e1.manager_id = emp.Emp_id where e1.salary > emp.salary
//Count employees under each manager
select manager_id, count(*) as totalemployes from Employee where manager_id is not null  group by manager_id
//Find total salary of employee reporting to each manager
select manager_id ,sum(salary) as salary from Employee where manager_id is not null group by manager_id
//Find average salart of employee under each manager 
select manager_id, avg(salary) as average_Salary from Employee group by manager_id
//Find highest salary of each manager 
select manager_id, max(salary) from Employee where manager_id is not null group by manager_id
//Having filter groups while where filter rows
//Show managers having more than 2 employee
select manager_id from Employee group by manager_id having count(emp_id)>=2
//show managers whose teams total salary is greater than 900
select manager_id from Employee group by manager_id having sum(salary)>1200
//show managers having exactly 2 employee
select manager_id from Employee group by manager_id having count(*)=2
//display managers names with the number of employees reporting to them
select (e1.emp_name) ,emp.manager_id ,count(*) as employees_reporting from Employee emp inner join employee e1 on emp.manager_id=e1.emp_id  group by  emp.manager_id ,e1.emp_name
//display manager name with total salary of team
select e1.emp_name ,sum(emp.salary) from Employee emp inner join employee e1 on emp.manager_id = e1.emp_id group by e1.emp_name
//find the manager whose team has the highest total salary
select e1.emp_name,sum(e1.salary) as ts from Employee emp inner join Employee e1 on emp.manager_id=e1.emp_id group by e1.emp_name  order by ts desc limit 1
//Find managers whose team average salary is greater than the companys average salary.
select e1.emp_name, avg(e1.salary) team_avg_Salary from Employee emp inner join Employee e1 on emp.manager_id = e1.emp_id group by e1.emp_name having avg(emp.salary)> (select avg(salary) from Employee)
//Find maximym salary of person under each manager
select manager_id ,max(salary) from Employee group by manager_id 









