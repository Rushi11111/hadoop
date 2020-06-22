HDFS and S3A I/O read time custom instrumentation.
Author and contact: Luca.Canali@cern.ch

This adds I/O time instrumentation to HDFS and S3A filesystems.
The proposed changes introduce I/O time instrumentation for S3AInputStream and for DFSInputStream.
Note, only read instrumentation is implemented so far

The instrumentation adds an API with counters in
- S3ATimeInstrumentation
- HDFSTimeInstrumentation

The jars modified by this change are:

hadoop-hdfs-client-3.2.0.jar
  -  hadoop-hdfs-project/hadoop-hdfs-client/target/hadoop-hdfs-client-3.2.0.jar
hadoop-aws-3.2.0.jar
  - hadoop-tools/hadoop-aws/target/lib/hadoop-hdfs-client-3.2.0.jar

The motivation of this work is to instrument I/O activity for Spark jobs, see:
  - https://github.com/cerndb/SparkPlugins

This work builds on similar work to instrument I/O for Hadoop-XRootD connector and OCI-HDFS connector in

- https://github.com/cerndb/hadoop-xrootd/blob/master/src/main/java/ch/cern/eos/XRootDInstrumentation.java
- https://github.com/LucaCanali/oci-hdfs-connector

This is currently a hack on top of Hadoop, it could enter mainstream in the future, see also
the work on HADOOP-1630 "Add public IOStatistics API; S3A to support"
https://issues.apache.org/jira/browse/HADOOP-16830

