✍️ 활동중인(Active) 부서의 현재 부서관리자(manager) 중 연봉 상위 5위안에 드는 사람들이 최근에 각 지역별로 언제 퇴실(O)했는지 조회해보세요.

```
SELECT manager.employee_id
	,  employee.last_name
	,  salary.annual_income
	,  `position`.position_name
	,  record.`time`
	,  record.region
	,  record.record_symbol
  FROM tuning.department
 INNER JOIN tuning.manager
    ON department.id = manager.department_id
 INNER JOIN tuning.employee
    ON manager.employee_id = employee.id
 INNER JOIN tuning.`position`
    ON manager.employee_id = `position`.id
 INNER JOIN tuning.record
    ON manager.employee_id = record.employee_id
 INNER JOIN tuning.salary
    ON manager.employee_id = salary.id
   AND salary.end_date LIKE '9999%'
 WHERE (department.note LIKE 'a%'
    OR department.note LIKE 'A%')
   AND manager.end_date LIKE '9999%'
   AND `position`.end_date LIKE '9999%'
   AND record.record_symbol = 'O'
 ORDER BY salary.annual_income DESC
        , record.`time` DESC
```
