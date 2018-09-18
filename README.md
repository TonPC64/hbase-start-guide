# HBASE START GUIDE (Standalone)
> how to start setup and run hbase standalone for dev
## Required
* [JAVA8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

## Installation 

## macOS
> Install java via .dmg from [download](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)


## Linux

```sh
# install java oracle 8
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer

# set default java
sudo apt-get install oracle-java8-set-default
```
---
## Set JAVA_HOME

> set JAVA_HOME in your shell profile (.zshrc, .bashrc)

find java_home by command on macOS
```sh
/usr/libexec/java_home
```

### macOS example
```sh
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_181.jdk/Contents/Home
```

### Linux example
```sh
export JAVA_HOME=/usr/lib/jvm/java-8-oracle
```

---

## HBASE

[Download HBASE Link](https://hbase.apache.org/downloads.html)

> Download bin not src
[https://www.apache.org/dyn/closer.lua/hbase/2.0.2/hbase-2.0.2-bin.tar.gz](https://www.apache.org/dyn/closer.lua/hbase/2.0.2/hbase-2.0.2-bin.tar.gz)

```sh
curl http://archive.apache.org/dist/hbase/2.0.2/hbase-2.0.2-bin.tar.gz -o hbase-2.0.2-bin.tar.gz
tar -xzvf hbase-2.0.2-bin.tar.gz
cd hbase-2.0.2
```

## Config HBASE

### hbase-env.sh
> set JAVA_HOME in file <b>conf/hbase-env.sh</b>
> uncomment JAVA_HOME and set your JAVA_HOME

### hbase-site.xml

> change testuser to your user in your machine

> best way to find your user just cd to ~(home) and run <b>pwd</b> for see path and copy that for replace /home/testuser 

example in macOS when run pwd in home
```
/Users/username
```

in Linux 
```
/home/username
```

example config hbase-site.xml

```xml
<configuration>
  <property>
    <name>hbase.rootdir</name>
    <value>file:///home/testuser/hbase</value>
  </property>
  <property>
    <name>hbase.zookeeper.property.dataDir</name>
    <value>/home/testuser/zookeeper</value>
  </property>
  <property>
    <name>hbase.unsafe.stream.capability.enforce</name>
    <value>false</value>
    <description>
      Controls whether HBase will check for stream capabilities (hflush/hsync).

      Disable this if you intend to run on LocalFileSystem, denoted by a rootdir
      with the 'file://' scheme, but be mindful of the NOTE below.

      WARNING: Setting this to false blinds you to potential data loss and
      inconsistent system state in the event of process and/or node failures. If
      HBase is complaining of an inability to use hsync or hflush it's most
      likely not a false positive.
    </description>
  </property>
</configuration>
```

---
## Start HBASE  
```sh
## start
./bin/start-hbase.sh
./bin/hbase shell

## stop 
./bin/stop-hbase.sh
```

### [Official Document HBASE standalone](http://hbase.apache.org/book.html#standalone)