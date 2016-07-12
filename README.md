# learn-at-work
Learn at work like commands, tips, best practices, etc

### Unix Commands:

$ nohup myscript.sh  (for No Hang UP)
$ ps axu | grep pchalla

### Hadoop:
1. Hadoop fs lookup for block size?
    $HADOOP_HOME/bin/hadoop fsck /path/to/file -files -blocks
2. Impala cannot see the table created in Hive
    Impala-shell> invalidate metadata;
3. cp vs distcp in Hadoop?
    - distcp will initiate mapreduce job - good for intracluster transfer. It runs in distributed mode. Good for large datasets (> 100GB)
    - use cp for small files (upto 50GB). cp is serialized and simpler. CP command is not parallel, It's just call FileSystem
    - if cluster is busy with other jobs distcp will wait for free map slots
4. if your hive query fails on snappy data on MacBook with message as "java.lang.UnsatisfiedLinkError: no snappyjava in java.library.path"
  ```
  git clone https://github.com/xerial/snappy-java.git
  cd snappy-java
  make

  cp target/snappy-java-1.1.1.3.jar $HADOOP_HOME/share/hadoop/common/lib/asnappy-java-1.1.1.3.jar
  ```
  During building the snappy-java, you may need to install below on Mac (as required)
  ```
  brew install automake
  brew install autoconf
  brew install libtool
  brew search pkg-config
  brew install pkg-config
  ```
