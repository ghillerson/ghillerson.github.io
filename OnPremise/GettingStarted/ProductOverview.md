[Open topic with navigation](../../index.html#OnPremise/GettingStarted/ProductOverview.html)

[]()A Technical Introduction to Splice Machine
==============================================

This section provides a technical overview of and introduction to Splice Machine. This introduction is for you if you are a database engineer or developer who wants to understand the scope of Splice Machine's feature set, so you can quickly zero in on what you need to learn without wading through too much extraneous material.

This section assumes that you have some familiarity with relational databases and SQL. We also assume that you know about clustered databases, and have some sense of what the Hadoop ecosystem provides for clusters. We will explain how Splice Machine leverages and fits into that ecosystem.

Splice Machine Open Source
--------------------------

Splice Machine is open source software.

For access to the full source code for Splice Machine, visit [our open source GitHub repository](https://github.com/splicemachine/spliceengine "Click to navigate to the Splice Machine Open Source GitHub repository (opens in new tab)"): 

Splice Machine Editions

To compare the features available in the Splice Machine Community and Enterprise Editions, please visit our <span class="ItalicFont">[Editions Summary](SpliceEditions.html)</span> page.

To obtain a license and activate the additional features in the Splice Machine <span class="ItalicFont">Enterprise Edition</span>, <span class="noteEnterpriseNote">please [Contact Splice Machine Sales](http://www.splicemachine.com/company/contact-us/) today.</span>

Splice Machine Clustered and Standalone Versions
------------------------------------------------

The following table summarizes the differences between the clustered and standalone versions of Splice Machine:

|              | Clustered Version of Splice Machine                                                                                                                                                                                                           | Standalone Version of Splice Machine                                                                                                                                                                                                                            |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Usage        | The <span class="ItalicFont">Clustered version</span> of Splice Machine allows a database to scale beyond terabytes and distribute data automatically across a cluster of machines, and is the production version that Splice Machine sells.  
                                                                                                                                                                                                                                                               
                There are different variations of our clustered version for different Hadoop platforms, including Cloudera, MapR, and Hortonworks, running on different Unix versions, including Ubuntu, CentOS, and RHEL.                                     | The standalone version installs quickly on your MacOS, Linux, or CentOS computer, and enables rapid access to Splice Machine's capabilities. It's an excellent way to experiment with Splice Machine with a reasonably small amount of data.                    
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 
                                                                                                                                                                                                                                                                Many of our customers also use a standalone version of Splice Machine for development work; specifically, when doing development work such as creating stored procedures. This allows developers to debug and optimize their work before updating your cluster.  |
| Downloading  | To download the clustered version of Splice Machine, you need to fill out the information request form on [our web site](http://www.splicemachine.com/company/contact-us/). We'll then contact you with download instructions.                | You can download the standalone version directly from Splice Machine by clicking the <span class="AppCommand">Download</span> button on [our web site](http://www.splicemachine.com/). You can use this version on MacOS and Linux computers.                   |
| Installing   | You need to spend about 30 minutes walking through the steps that are described in our [Splice Machine Installation Guide](../InstallingSpliceMachine/Intro.InstallationGuide.html) to install and configure Splice Machine.                  | Download the installer and follow the instructions in our [Splice Machine Installation Guide](../InstallingSpliceMachine/Intro.InstallationGuide.html).                                                                                                         |
| Requirements | See our [Requirements](Requirements.html) page.                                                                                                                                                                                               | See our [Requirements](Requirements.html) page.                                                                                                                                                                                                                 |

The remainder of this section includes these topics:

-   An [Architectural Overview](ArchitectureOvervew.html) of Splice Machine, including a brief summary of Hadoop and of how Splice Machine fits into the Hadoop ecosystem.
-   A summary of [Splice Machine Features](FeatureOvervew.html) that you should know about with links to more detailed descriptions elsewhere in our documentation.
-   A brief description of how to perform [Common Tasks in Splice Machine.](TaskOverview.html)

 


