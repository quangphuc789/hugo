+++
date = "2016-09-03T02:02:05+08:00"
title = "Simple Usage of JOIN and RANK in SQL"
draft = false
tags = ['sql']
categories = ["Software Engineering"]

+++

When retrieving data from SQL tables, sometimes there is a real need to retrieve the row indexes of the data within the table itself. To understand more about this usage, consider a small example/circumstance below:

**Description**

Imagine you need to create a simple `SELECT` statement that will return all columns from the `people` table, and join to the `sales` table so that you can return the total of all `sales` and rank each person by their `sale_count`.

*people* table schema:

    id  
    name

*sales* table schema:

    id      
    people_id   
    sale     
    price    

Then return all people fields as well as the sale count as `sale_count` and the rank as `sale_rank`.

**My Solution**

*1. Define your SELECT columns*

Firstly, the requirement

    SELECT 
      p.id,
      p.name,
      COUNT(s.id) as sale_count,
      ROW_NUMBER() OVER (ORDER BY COUNT(s.id) DESC) as sale_rank
    FROM
      people p
      JOIN sales s
      ON p.id = s.people_id
    GROUP BY
      p.id