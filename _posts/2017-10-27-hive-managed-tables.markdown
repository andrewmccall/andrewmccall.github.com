---
layout: post
title:  "Hive, managed vs external tables"
date:   2017-10-27 18:00:00 +0000
author: Andrew McCall
cover: /images/post_images/hive.jpeg
categories: bigdata hive hadoop
---

One of the things that comes up often in conversations about Hive is using
managed vs. external tables.

# What are managed tables?

Managed tables are Hive tables where Hive manages the data; Hive stores the
data internally in it's own warehouse directory and generally you wouldn't
interact with the data directly.

On of the key things to know about managed tables is that if you drop the table
you're dropping the metadata *AND* the data.

# What are external tables?

External tables are Hive tables where the data is managed external to Hive. An
example would be a folder full of files with a schmea applied on top. You can
add and remove files to the folder and the contents will be added to the Hive tables.

When you drop an external table, you're only dropping the metadata the underlying
data will still exist in HDFS.

External table files are also accessible via HDFS and security needs to be managed at the HDFS file/folder level.

# When to use them?

Beyond the general answer of "It depends on your use case", some pointers that
I'd give are:

## External Tables

* The data is used or created  outside of Hive. Examples include landing raw files or needing the data to process elsewhere.
* You don't want a DROP TABLE to delete the data. Examples include creating a number
of schemas using the same underlying dataset or creating a partial schema on some data which may be evolving.

## Managed Tables

* The data is temporary.
* The data in the table is completely derived from other Hive tables.
