[Open topic with navigation](../../index.html#OnPremise/GettingStarted/Requirements.html)

[]()[]()Splice Machine Requirements
===================================

This topic summarizes the hardware and software requirements for Splice Machine running on a cluster or on a standalone computer.

[]()[]()Cluster Node Requirements
---------------------------------

The following table summarizes the minimum requirements for the nodes in your cluster:

| Component                          | Requirements                                                                                                                                                                                                                                                                                                                  |
|------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cores                              | Splice Machine recommends that each node in your cluster have 8-12 hyper-threaded cores (16-32 hyper-threads) for optimum throughput and concurrency.                                                                                                                                                                         |
| Memory                             | We recommend that each machine in your cluster have at least 64 GB of available memory.                                                                                                                                                                                                                                       |
| Disk Space                         | Your root drive needs to have at least 100 GB of free space.                                                                                                                                                                                                                                                                  
                                                                                                                                                                                                                                                                                                                                                                     
                                      Splice Machine recommends separate data drives on each cluster node to maintain a separation between the operating system and your database data. You need capacity for a minimum of three times the size of the data you intend to load; the typical recommended configuration is 2 TB or more of attached storage per node.  
                                                                                                                                                                                                                                                                                                                                                                     
                                      <span class="BoldFont">Your data disks should be set up with a single partition and formatted with an <span class="CodeFont">ext4</span> file system.</span>                                                                                                                                                                   |
| Hadoop Ecosystem                   | The table in the next section, Hadoop Ecosystem Requirements, summarizes the specific Hadoop component versions that we support in each of our product releases.                                                                                                                                                              |
| Software Tools and System Settings | The <span class="ItalicFont">Linux Configuration</span> topic in each section of our <span class="ItalicFont">Installation Guide</span> that pertains to your installation summarizes the software tools and system settings required for your cluster machines.                                                              |

### Amazon Web Services (AWS) Requirements

If you're running on AWS, your cluster must meet these minimum requirements:

| Component            | Requirements                                                                         |
|----------------------|--------------------------------------------------------------------------------------|
| Minimum Cluster Size | The minimum cluster size on AWS is <span class="ItalicFont">5 nodes</span>:          
                                                                                                              
                        -   1 master node                                                                     
                        -   4 worker nodes                                                                    |
| Minimum Node Size    | Minimum recommended size of each node is <span class="ItalicFont">m4.4xlarge</span>. |
| Disk Space           | Minimum recommended storage space:                                                   
                                                                                                              
                        -   <span class="ItalicFont">100GB</span> EBS root drive                              
                        -   4 EBS data drives per node                                                        
                                                                                                              
                        Note that the required number of data drives per node depends on your use case.       |

### []()Hadoop Ecosystem Requirements

The following table summarizes the required Hadoop ecosystem components for your platform:

Splice Machine
Hadoop platform
Linux
Hadoop
HBase
ZooKeeper
<span class="BoldFont">Release 2.5</span>
<span class="PlatformVariablesCDH5Versions">CDH 5.7.2, 5.8.0, 5.8.3</span>
<span class="PlatformVariablesCDH5OS">CentOS/RHEL 6</span>

<span class="PlatformVariablesCDH5Hadoop">2.6.0</span>
<span class="PlatformVariablesCDH5HBase">1.0.0</span>
<span class="PlatformVariablesCDH5Zookeeper">3.4.5</span>
<span class="PlatformVariablesHDP2Versions">HDP 2.4.2 and 2.5</span>
<span class="PlatformVariablesHDP2OS">CentOS/RHEL 6</span>

<span class="PlatformVariablesHDP2Hadoop">2.7.1</span>
<span class="PlatformVariablesHDP2HBase">1.1.2</span>
<span class="PlatformVariablesHDP2Zookeeper">3.4.5</span>
<span class="PlatformVariablesMapR5Versions">MapR 5.1.0 and 5.2.0</span>
<span class="PlatformVariablesMapr5OS">CentOS/RHEL 6</span>

<span class="PlatformVariablesMapr5Hadoop">2.7.0</span>
<span class="PlatformVariablesMapr5HBase">1.1.1</span>
<span class="PlatformVariablesMapr5Zookeeper">3.4.5</span>
 
<span class="BoldFont">Release 2.0</span>
<span class="PlatformVariablesSplice20CDH5Versions">CDH 5.6 or CDH 5.5.2</span>
<span class="PlatformVariablesCDH5OS">CentOS/RHEL 6</span>

<span class="PlatformVariablesCDH5Hadoop">2.6.0</span>
<span class="PlatformVariablesCDH5HBase">1.0.0</span>
<span class="PlatformVariablesCDH5Zookeeper">3.4.5</span>
<span class="PlatformVariablesSplice20HDP2Versions">HDP 2.4.2</span>
<span class="PlatformVariablesHDP2OS">CentOS/RHEL 6</span>

<span class="PlatformVariablesHDP2Hadoop">2.7.1</span>
<span class="PlatformVariablesHDP2HBase">1.1.2</span>
<span class="PlatformVariablesHDP2Zookeeper">3.4.5</span>
<span class="PlatformVariablesSplice20MapR5Versions">MapR 5.1.0</span>
<span class="PlatformVariablesMapr5OS">CentOS/RHEL 6</span>

<span class="PlatformVariablesMapr5Hadoop">2.7.0</span>
<span class="PlatformVariablesMapr5HBase">1.1.1</span>
<span class="PlatformVariablesMapr5Zookeeper">3.4.5</span>
### Java JDK Requirements

Splice Machine supports the following versions of the Java JDK:

-   Oracle JDK 1.8, update 60 or higher

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>We recommend that you do not use JDK 1.8.0\_40

Splice Machine does not test our releases with OpenJDK, so we recommend against using it.

[]()[]()Standalone Version Prerequisites
----------------------------------------

You can use the standalone version of Splice Machine on MacOS and Linux computers that meet these basic requirements:

| Component                                      | Requirements                                                                                                                                                                                                        |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span class="BoldFont">Operating System</span> | Mac OS X, version 10.8 or later,                                                                                                                                                                                    
                                                                                                                                                                                                                                                                       
                                                  CentOS 6.4 or equivalent.                                                                                                                                                                                            |
| <span class="BoldFont">CPU</span>              | Splice Machine recommends 2 or more multiple-core CPUs.                                                                                                                                                             |
| <span class="BoldFont">Memory</span>           | At least 16 GB RAM, of which at least 10 GB is available.                                                                                                                                                           |
| <span class="BoldFont">Disk Space</span>       | At least 100 GB of disk space available for Splice Machine software, plus as much space as will be required for your data; for example, if you have a 1 TB dataset, you need at least 1 TB of available data space. |
| <span class="BoldFont">Software</span>         | You must have JDK installed on your computer.                                                                                                                                                                       |

 


