+++
title = "MongoDB Track Creation Time Of Document"
date = "2016-02-23T14:27:57+08:00"
draft = false
tags = ["mongodb"]
categories = ["Software Engineering"]

+++

Developers need good ways to keep track of records creation time in database systems. In MongoDB, the best way to track document creation time is actually not creating anything at all. MongoDB keeps this information automatically in its ObjectID.

The field [_id] in MongoDB is the proper way it identifies unique documents across the whole system. But it is not simply an ID in the form of a string. It is actually an object, ObjectID object. This object holds the creation time of the object itself.

```
$object = new MongoDBObject;
$object->save();
$time = $object['_id']->getTimestamp();
var_dump(date('r', $time));
```