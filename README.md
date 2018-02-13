HDFS for Go
===========

This is just a fork from [github.com/colinmarc/hdfs](https://github.com/colinmarc/hdfs), take a look there for better information.


This fork add the functionality to perform append operations to files that perhaps don't exist, creating them in that case:
```go
package main

import (
        "log"

        "github.com/mcarmonaa/hdfs"
)

const (
        namenode = "localhost:8020"
        path     = "/hello.world"
)

func main() {
        client, err := hdfs.New(namenode)
        if err != nil {
                log.Fatal(err)
        }

        writer, err := client.AppendOrCreate(path)
        if err != nil {
                log.Fatal(err)
        }
        defer writer.Close()

        writer.Write([]byte("Hello World! ---> Appending this line!\n"))
}

```
Installing the library
----------------------

To install the library, once you have Go [all set up][2]:

    $ go get -u github.com/mcarmonaa/hdfs

Environment variables
---------------------------------

You'll want to add the following line to your `.bashrc` or `.profile`:

    export HADOOP_NAMENODE="namenode:8020"

By default, the HDFS user is set to the currently-logged-in user. You can
override this in your `.bashrc` or `.profile`:

    export HADOOP_USER_NAME=username

Compatibility
-------------

This library uses "Version 9" of the HDFS protocol, which means it should work
with hadoop distributions based on 2.2.x and above. The tests run against CDH
5.x and HDP 2.x.
