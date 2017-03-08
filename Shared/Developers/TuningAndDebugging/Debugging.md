[Open topic with navigation](../../../index.html#Shared/Developers/TuningAndDebugging/Debugging.html)

Debugging Splice Machine
========================

This topic describes the parameter values you need to know for debugging Splice Machine with a software tool:

-   Create a configuration in your software to remotely attach to Splice Machine
-   Connect to port <span class="CodeFont">4000</span>.

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>If you're debugging code that is to be run in a Spark worker, connect to port <span class="CodeFont">4020</span> instead.

Example

Here's an example of an <span class="ItalicFont">IntelliJ IDEA</span> debugging configuration using port <span class="CodeFont">4000</span>:

<img src="../../../Resources/Images/DebugSetupScreen.png" title="Sample configuration for debugging Splice Machine with IntelliJ IDEA" alt="Sample configuration for debugging Splice Machine with IntelliJ IDEA" class="indentedTightSpacing" />

For access to the full source code for Splice Machine, visit [our open source GitHub repository](https://github.com/splicemachine/spliceengine "Click to navigate to the Splice Machine Open Source GitHub repository (opens in new tab)"):  https://github.com/splicemachine/spliceengine

 


