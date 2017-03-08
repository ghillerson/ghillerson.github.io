[Open topic with navigation](../../index.html#OnPremise/InstallingSpliceMachine/Intro.InstallationGuide.html)

Splice Machine Installation Guide
=================================

This <span class="ItalicFont">Installation Guide</span> walks you through installing Splice Machine on your cluster, or on computer if you're using the standalone version.

The fastest way to get started with Splice Machine is to set up our sandbox on the Amazon Web Services (AWS) platform on EC2 instances using <span class="CodeFont">cloud.splicemachine.com</span>:

See the [Installing Splice Machine on Amazon Web Services](AWSSandbox.html) topic in this chapter for step-by-step instructions for setting up the Splice Machine sandbox.

If you want to download and install Splice Machine on your cluster or standalone computer, please read the remainder of this page, which includes these sections:

-   The Cluster Node Requirements section below details the hardware and ecosystem requirements for installing Splice Machine on a cluster or on a standalone computer.
-   The [Configure Linux for Splice Machine](#Configur) section specifies the Linux software that Splice Machine requires.
-   The [Install Splice Machine](#Install) links to the platform-specific installation page for each version of Splice Machine.

Installing the Splice Machine Sandbox on AWS
--------------------------------------------

The fastest way to get started with Splice Machine is to set up our sandbox on the Amazon Web Services (AWS) platform on EC2 instances using <span class="CodeFont">cloud.splicemachine.com</span>.
See the [Installing Splice Machine on Amazon Web Services](AWSSandbox.html) topic in this chapter for step-by-step instructions.

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

[]()Configure Linux for Splice Machine
--------------------------------------

The following table summarizes Linux configuration requirements for running Splice Machine on your cluster:

| Configuration Step                             | Description                                                                                                                                                                     |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Configure SSH access:                          | Configure the user account that you're using for cluster administration for password-free access, to simplify installation.                                                     |
| Configure swappiness:                          | ``` ShellCommandCell                                                                                                                                                            
                                                  echo 'vm.swappiness = 0' >> /etc/sysctl.conf                                                                                                                                     
                                                  ```                                                                                                                                                                              |
| If you are using Ubuntu:                       | ``` ShellCommandCell                                                                                                                                                            
                                                  rm /bin/sh ; ln -sf /bin/bash /bin/sh                                                                                                                                            
                                                  ```                                                                                                                                                                              |
| If your using CentOS or RHEL:                  | ``` ShellCommandCell                                                                                                                                                            
                                                                                      sed -i '/requiretty/ s/^/#/' /etc/sudoers                                                                                                    
                                                  ```                                                                                                                                                                              |
| Required software:                             | Verify that the following set of software (or packages) is available on each node in your cluster:                                                                              
                                                                                                                                                                                                                                   
                                                  -   curl                                                                                                                                                                         
                                                  -   jdk-1.7.0\_XX (Oracle JDK v1.7.0)                                                                                                                                            
                                                                                                                                                                                                                                   
                                                      <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You may your platform management software (re-install) JDK 1.7 during its own installation process.  
                                                                                                                                                                                                                                   
                                                  -   nscd                                                                                                                                                                         
                                                  -   ntp                                                                                                                                                                          
                                                  -   openssh, openssh-clients<span class="bodyFont">, and</span> openssh-server                                                                                                   
                                                  -   patch                                                                                                                                                                        
                                                  -   rlwrap                                                                                                                                                                       
                                                  -   wget                                                                                                                                                                         |
| Additional required software on CentOS or RHEL | If you're running on CENTOS or RHEL, you also need to have this software available on each node:                                                                                
                                                                                                                                                                                                                                   
                                                  -   ftp                                                                                                                                                                          
                                                  -   EPEL <span class="bodyFont">repository</span>                                                                                                                                |
| Services that must be started                  | You need to make sure that the following services are enabled and started:                                                                                                      
                                                                                                                                                                                                                                   
                                                  -   <span class="CodeFont">nscd</span>                                                                                                                                           
                                                  -   <span class="CodeFont">ntpd</span> (<span class="CodeFont">ntp</span> package)                                                                                               
                                                  -   <span class="CodeFont">sshd</span> (<span class="CodeFont">openssh</span>-server package)                                                                                    |
| Time zone setting                              | <span class="Highlighted">Make sure all nodes in your cluster are set to the same time zone.</span>                                                                             |

[]()Install Splice Machine
--------------------------

If you've decided to try our sandbox, see the [Installing Splice Machine on Amazon Web Services](AWSSandbox.html) topic in this chapter for step-by-step instructions for setting up the Splice Machine sandbox.     

To install Splice Machine on your cluster or standalone computer, click the link below to see the instructions for your platform; each page walks you through downloading and installing and configuring a specific version of Splice Machine:

| Hadoop Platform                      | Installation Guide                                                                |
|--------------------------------------|-----------------------------------------------------------------------------------|
| Cloudera-managed cluster             | [Installing and Configuring Splice Machine for Cloudera Manager](CDHInstall.html) |
| Hortonworks-managed cluster          | [Installing and Configuring Splice Machine for Hortonworks HDP](HDPInstall.html)  |
| MapR-managed cluster                 | [Installing and Configuring Splice Machine for MapR](MapRInstall.html)            |
| Standalone version of Splice Machine | [Installing the Standalone Version of Splice Machine](StandaloneInstall.html)     |

For access to the full source code for Splice Machine, visit [our open source GitHub repository](https://github.com/splicemachine/spliceengine "Click to navigate to the Splice Machine Open Source GitHub repository (opens in new tab)"): 

 


