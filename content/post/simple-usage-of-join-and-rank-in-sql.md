+++
date = "2016-09-03T02:02:05+08:00"
title = "Simple Usage of JOIN and ROW_NUMBER in SQL"
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

**My Solution & Step-By-Step Walkthrough**

*1. Prepare your FROM cross reference dataset*

First, prepare the data set. Clearly that `people.id` and `sales.people_id` are referenced, in both naming convention and their actual meanings.

    FROM
      people p
      JOIN sales s
      ON p.id = s.people_id

Good practice is to always name table variables.

*2. Define your SELECT criteria*

Next, the requirement asks us to return **all** the fields in `people` table. Therefore, selecting everything from `people` is apparent. Secondly, we need something as `sale_count` (sum of all sale deals) and something else as `sale_rank` (ranking of this person). We will figure those *something else* later. We start off with:

    SELECT
      p.id,
      p.name,
      <something A> as sale_count,
      <something B> as sale_rank

Here, I do not want to use `p.\*`, even though I could, because that is a bad practice. The reason is, no one guarantees the structure of `people` remains over the years. A good database architect/developer will practically add more columns if he needs to, and avoid removing/altering table columns. Therefore, p.`* will potentially add more columns in secret. Clearly there is no error reporting to the developer, until the end users figure it out. But that is bad.

If specifying the columns in details, even when the columns are removed/altered, there will be error reported to the developer. And that will be easily fixed.

*3. Extra Viewing Requirement*

Since the question asked us to return people, there is an assumption that there is no duplicate people. Use `GROUP BY` for unifying non-duplicating people:

    GROUP BY
      p.id

*4. Missing Logic*

*something A* is a total sum of sale deals of a person. So we can understand it as total of repeat rows that appear on our prepared dataset, on each person (since 1 person can make multiple sale deals). We need to sum them all, use aggregate function `COUNT` for this purpose. So, *something A* can be replaced by `COUNT(s.id)`

*something B* is a little more tricky. The idea is, we can sort rows by using `ORDER BY`, after that, use the exact row id for the ranking. For the row id, use `ROW_NUMBER() OVER()`. Inside `OVER()` logic, order the rows as `ORDER BY COUNT(s.id) DESC`.

So we have:

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

Note that ROW_NUMBER() functions as same as RANK().