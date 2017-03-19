+++
date = "2016-04-03T02:02:05+08:00"
title = "Simple Usage of JOIN and RANK in SQL"
draft = false
tags = ['sql']
categories = ["Software Engineering"]

+++

***Description:***

Imagine you need to create a simple SELECT statement that will return all columns from the people table, and join to the sales table so that you can return the COUNT of all sales and RANK each person by their sale_count.

*people* table schema

id
name


*sales* table schema

id
people_id
sale
price

Then return all people fields as well as the sale count as "sale_count" and the rank as "sale_rank".
