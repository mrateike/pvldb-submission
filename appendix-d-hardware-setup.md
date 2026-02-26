# Appendix D: Hardware and Train/Test Setup

## Cluster Hardware Configuration

The data collection and model evaluation hardware configuration includes 20 OpenShift worker nodes, each equipped with 4 x Intel Xeon E5-2683 v4 CPUs running at 2.10 GHz (16 cores per CPU, 64 physical cores per node), 1.5 TB of RAM, and 128 GB NVMe local storage. Hyper-Threading is enabled, providing 128 logical CPUs per node. The nodes are interconnected using dual 25 Gbit Ethernet links. Persistent data is stored on an S3-compatible object store accessed via the S3A connector.

## Data Processing Infrastructure

Our data processing infrastructure leverages Apache Spark 3.5.4 integrated with Iceberg as the underlying table format. Iceberg is configured with a Hive-backed catalog and an external Hive Metastore for metadata management while table data is stored in S3-compatible object storage accessed via the S3A connector. The execution engine is accelated using Gluten with the Velox native backend, enabling columnar execution and native vectorized processing.

## Train/Test Configurations

For Training, we shut down an executor after 60 seconds of idleness, following the default \Apache\ configuration. The maximum available number of executors is 128. For testing, Apache Spark queries Mira for updates on the recommended number of cores computed by our optimization framework at 300‑millisecond intervals. Multiple stages may run in parallel as long as their combined recommended executors remain within a limit of 128 executors. For our methods and CherryPick, any executor that becomes idle is shut down immediately when no further tasks remain for its active stage. The Apache Spark baseline uses the default 60‑second executor idle timeout.