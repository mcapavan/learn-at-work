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

### Ambari is unable to create users as no one has access to /home directory in OS level due to NetApp

you can change the default OS-level home folder base from /etc/default/useradd, this way all new users added by ambari will have their home folder correctly set as they are created

```bash
sed -i 's|^HOME=.*$|HOME=/hadoop/home|g' /etc/default/useradd
```

If customer doesn't want to make changes, then create all the required used by Ambari and set ignore_groupsusers_create=true in cluster-env.xml 

ref: https://community.hortonworks.com/articles/89406/is-it-possible-to-change-the-home-directory-of-hdp.html

### Migrate Hive Saved Queries from Hue to Ambari Hive View from two different clusters

1. Get all the user saved queries from Hue Database

```text
select useradmin_userprofile.home_directory, beeswax_savedquery.data 
from useradmin_userprofile, beeswax_savedquery 
where useradmin_userprofile.user_id = beeswax_savedquery.owner_id and beeswax_savedquery.is_auto=1;
```


