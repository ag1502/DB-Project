Parallelized Query Optimization for Joins
=========================================

Functionalities Provided
------------------------

1. Primary:
```	
	SELECT * FROM  Q1, Q2, Q3, …, Qn WHERE P1, P2, P3,P4
```
where Qi are the tables and Pi are the predicates on attributes in tables

2. Optional: Right now, in our vanilla implementation, we will be only trying to optimize one type of scans and a particular implementation of join methods. If we have time, the we could try to incorporate the various join methods and scan methods into an improved cost function which will give a better plan.
As of now, we haven’t promised to handle special kinds of joins such as Left Join since there planning is handled differently in Postgresql. We can try to overcome this.


Limitations
-----------

1. For bushy tree joins we require number of relations to be 0 mod 3 and for left deep we require the number of relations to be 0 mod 2.

2. The maximum number of workers for left deep join is 2^((num_relations)/2) and for bushy is 2^((num_relations)/3). In case where the actual number of workers exceeds above, the remaining workers would not be initiated. 

3. We have used locks in some critical PostgreSql functions (palloc) for addressing concurrency issues. Even then, for large number of workers we have some concurrency related bugs. If we further serialize the worker threads by adding locks, the issue is resolved at the cost of parallelism.


Bibliography
------------

Query Optimisation on Shared Nothing Architectures
http://www.vldb.org/pvldb/vol9/p660-trummer.pdf


Environment Variables
---------------------

export PATH=$HOME/postgresql/bin:$PATH
export PGDATA=$HOME/postgresql/dbdir
export LD_LIBRARY_PATH=$HOME/postgresql/lib

PostgreSQL Database Management System
-------------------------------------

This directory contains the source code distribution of the PostgreSQL
database management system.

PostgreSQL is an advanced object-relational database management system
that supports an extended subset of the SQL standard, including
transactions, foreign keys, subqueries, triggers, user-defined types
and functions.  This distribution also contains C language bindings.

PostgreSQL has many language interfaces, many of which are listed here:

	https://www.postgresql.org/download

See the file INSTALL for instructions on how to build and install
PostgreSQL.  That file also lists supported operating systems and
hardware platforms and contains information regarding any other
software packages that are required to build or run the PostgreSQL
system.  Copyright and license information can be found in the
file COPYRIGHT.  A comprehensive documentation set is included in this
distribution; it can be read as described in the installation
instructions.

The latest version of this software may be obtained at
https://www.postgresql.org/download/.  For more information look at our
web site located at https://www.postgresql.org/.
