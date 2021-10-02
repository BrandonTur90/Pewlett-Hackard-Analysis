# Pewlett-Hackard-Analysis

## Overview

The purpose of this analysis was to use postgres and SQL to identify how many
Pewlett-Hackard employees were close to retirement, which departments would be
most affected, and look for mentorship candidates to ease the loss in labor power.

## Results

![retiring_titles](/Images/retiring_titles.PNG)

* The above table shows how many employees of each title are at the retirement age,
  over ninety-thousand in total.
* Pewlett-Hackard stands to lose senior engineers and staff the most by a large amount
  over other titles.
* With such an outflux of expertise it was prudent to find employees that had expertise
  and could be mentored to fill the roles of those possibly retiring.
* Over 1,500 employees eligible for mentorship were identified. Below is a table that shows the
  results by title.

![mentor_title_count](/Images/mentor_title_count.PNG)

## Summary

As stated above, over 90,000 employees are close to or at the retirement age. Although 
there are about 1,500 employees eligible for mentorship, that's not going to fill the
roles. It would be worth expanding the birth date eligibility criteria another ten years 
to bring in younger employees to fill the gaps. Another option would be to determine
mentee eligibilty by hire date instead of birth date. Below are two example querries; one
for each idea.

Expand the birth date criteria:

```
SELECT 	DISTINCT ON (emp_no) e.emp_no,
		e.first_name,
		e.last_name,
		e.birth_date,
		de.from_date,
		de.to_date,
		t.title
INTO table
FROM employees as e
INNER JOIN dept_emp as de
ON (e.emp_no = de.emp_no)
INNER JOIN titles as t
ON (e.emp_no = t.emp_no)
WHERE (de.to_date = '9999-01-01')
AND (birth_date BETWEEN '1965-01-01' AND '1975-12-31')
ORDER BY e.emp_no;
```

Expand criteria by hire date:

```
SELECT 	DISTINCT ON (emp_no) e.emp_no,
		e.first_name,
		e.last_name,
		e.hire_date,
		de.to_date,
		t.title
INTO table
FROM employees as e
INNER JOIN dept_emp as de
ON (e.emp_no = de.emp_no)
INNER JOIN titles as t
ON (e.emp_no = t.emp_no)
WHERE (de.to_date = '9999-01-01')
AND (hire_date BETWEEN '1995-01-01' AND '9999-01-01')
ORDER BY e.emp_no;
```

