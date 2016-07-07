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
