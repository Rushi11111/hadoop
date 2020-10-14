HDFS and S3A I/O read time custom instrumentation.
Author and contact: Luca.Canali@cern.ch

This adds I/O time instrumentation to HDFS and S3A filesystems.
The proposed changes introduce I/O time instrumentation for S3AInputStream and for DFSInputStream.
Note, only read instrumentation is implemented so far

The instrumentation adds an API with counters:
- S3ATimeInstrumentation
  - timeElapsedReadMusec
  - timeElapsedSeekMusec
  - timeCPUDuringReadMusec
  - timeCPUDuringSeekMusec
  - timeGetObjectMetadata
  - timeCPUGetObjectMetadata
  - bytesRead
- HDFSTimeInstrumentation
  - timeElapsedReadMusec
  - timeCPUDuringReadMusec
  - bytesRead

The jars modified by this change are:

- hadoop-hdfs-client-3.2.0.jar
  - relative path: hadoop-hdfs-project/hadoop-hdfs-client/target/hadoop-hdfs-client-3.2.0.jar
  - download a pre-built copy of the [hadoop-hdfs-client-3.2.0.jar at this link](https://cern.ch/canali/res/hadoop-hdfs-client-3.2.0.jar)
- hadoop-aws-3.2.0.jar
  - relative path: hadoop-tools/hadoop-aws/target/hadoop-aws-3.2.0.jar
  - download a pre-built copy of the [hadoop-aws-3.2.0.jar at this link](https://cern.ch/canali/res/hadoop-aws-3.2.0.jar)

The motivation of this work is to instrument I/O activity for Spark jobs, see:
  - https://github.com/cerndb/SparkPlugins
  - Note: this repo modifies Hadoop (client) version 3.2.0, because that is the Hadoop version used by Apache Spark 3.0.

This work builds on similar work to instrument I/O for Hadoop-XRootD connector and OCI-HDFS connector in

- https://github.com/cerndb/hadoop-xrootd/blob/master/src/main/java/ch/cern/eos/XRootDInstrumentation.java
- https://github.com/LucaCanali/oci-hdfs-connector

This is currently a hack on top of Hadoop, it could enter mainstream in the future, see also
the work on HADOOP-1630 "Add public IOStatistics API; S3A to support"
https://issues.apache.org/jira/browse/HADOOP-16830

