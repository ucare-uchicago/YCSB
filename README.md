<!--
Copyright (c) 2010 Yahoo! Inc., 2012 - 2016 YCSB contributors.
All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License"); you
may not use this file except in compliance with the License. You
may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
implied. See the License for the specific language governing
permissions and limitations under the License. See accompanying
LICENSE file.
-->

UCARE UCHICAGO
====================================
This is our for of YCSB 0.15.0. The following bindings have been modified:

1. Core

This should affect all bindings. I have added a new value generator, the idea is that when inserting a key value pair, while the key generator remains unchanged, the value is generated from a pattern. The pattern is specified as:

valuefieldpattern=--some pattern--
  
and this property goes in the workload configuration file. So now, when inserting some key-value pair, the value will be generated using the chars in this pattern. For example, if fieldsize = 10 and pattern = abcd then the row will look like <id>,abcdabcdab.
  
This was tested for cassandra binding and it works fine as long as you dont need to check for data integrity (its not implemented, but should be relatively easy to do so).

The changes are in the following files:

 -- added com.yahoo.ycsb.FixedPatternByteIterator
 
 -- modified com.yahoo.ycsb.workloads.CoreWorkload

Look for @@cesar if you want to know which places were modified.







Yahoo! Cloud System Benchmark (YCSB)
====================================
[![Build Status](https://travis-ci.org/brianfrankcooper/YCSB.png?branch=master)](https://travis-ci.org/brianfrankcooper/YCSB)

Links
-----
http://wiki.github.com/brianfrankcooper/YCSB/  
https://labs.yahoo.com/news/yahoo-cloud-serving-benchmark/
ycsb-users@yahoogroups.com  

Getting Started
---------------

1. Download the [latest release of YCSB](https://github.com/brianfrankcooper/YCSB/releases/latest):

    ```sh
    curl -O --location https://github.com/brianfrankcooper/YCSB/releases/download/0.14.0/ycsb-0.14.0.tar.gz
    tar xfvz ycsb-0.14.0.tar.gz
    cd ycsb-0.14.0
    ```
    
2. Set up a database to benchmark. There is a README file under each binding 
   directory.

3. Run YCSB command. 

    On Linux:
    ```sh
    bin/ycsb.sh load basic -P workloads/workloada
    bin/ycsb.sh run basic -P workloads/workloada
    ```

    On Windows:
    ```bat
    bin/ycsb.bat load basic -P workloads\workloada
    bin/ycsb.bat run basic -P workloads\workloada
    ```

  Running the `ycsb` command without any argument will print the usage. 
   
  See https://github.com/brianfrankcooper/YCSB/wiki/Running-a-Workload
  for a detailed documentation on how to run a workload.

  See https://github.com/brianfrankcooper/YCSB/wiki/Core-Properties for 
  the list of available workload properties.

Building from source
--------------------

YCSB requires the use of Maven 3; if you use Maven 2, you may see [errors
such as these](https://github.com/brianfrankcooper/YCSB/issues/406).

To build the full distribution, with all database bindings:

    mvn clean package

To build a single database binding:

    mvn -pl com.yahoo.ycsb:mongodb-binding -am clean package
