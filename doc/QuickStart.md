QuickStar
======================

Good tools make system performance tuning quicker, easier and cheaper than if everything is done manually or by experience.

Bestconfig can find better configurations for a specific large-scale system deployed for a given application workload.

Overview
-----------------------

<div align=center>
    <br />
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/BestConfig.png" width = "600" height = "200" align=center />
    <p align=center>Deployment architecture </p>
</div>

Here, "deployment environment" refers to the actual running environment of your applications, while "staging environment" is some environment that is almost the same as the deployment environment but where tests are run without interfering the actual application.

<div align=center>
    <br />
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/deploy_process.jpg" width = "600" height = "340" align=center />
</div>
<div>
<p align=center>The process of deploying BestConfig </p>
</div>

The following part illustrates the detailed method of using BestConfig to tune practical systems by a case of spark tuning.

Spark tuning by BestConfig
--------------------------
Shell scripts
-------------
There are 9 shell scripts in BestConfig and they are classified into two groups.<br />
1. One group consits of 5 shell scripts, start.sh, isStart.sh, stop.sh, isClosed.sh and terminateSystem.sh, which are deployed on the      systems under test. <br />
  <div align=center>
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/shells-tune.jpg" width = "200" height = "100" align=center />
</div>
<br />
The scripts of start.sh and stop.sh deployed on worker and Master node are different. <br />  
<p>(1) Shell scripts (start.sh and stop.sh) on Master node</p>
<div align=center>
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/start.jpg"  align=center />
</div>
<p align=center>start.sh(Master)</p>
<div align=center>
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/stop.jpg"  align=center />
</div>
<p align=center>stop.sh(Master)</p>
<p>(2) Shell scripts (start.sh and stop.sh) on Worker node</p>
<div align=center>
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/start_worker.jpg" align=center />
</div>
<p align=center>start.sh(Worker)</p>
<div align=center>
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/stop_worker.jpg" align=center />
</div>
<p align=center>stop.sh(Worker)</p>
<div align=center>
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/isStart.jpg" align=center />
</div>
<p align=center>isStart.sh</p>
<p>(3) Identical shell scripts on Master and Worker node</p>
<div align=center>
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/terminateSystem.jpg"  align=center />
</div>
<p align=center>terminateSystem.sh</p>
<div align=center>
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/isClosed.jpg" align=center />
</div>
<p align=center>isClosed.sh</p>
2. Another group consits of 4 shell scripts, startTest.sh, getTestResult.sh, terminateTest.sh and isFinished.sh, which are deployed        on the test node. <br />
   <div align=center>
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/shell-test.jpg"  align=center />
</div>
<br />
<div align=center>
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/startTest.jpg"  align=center />
</div>
<p align=center>startTest.sh</p>
<div align=center>
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/isFinished.jpg"  align=center />
</div>
<p align=center>isFinished.sh</p>
<div align=center>
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/getTestResult.jpg"  align=center />
</div>
<p align=center>getTestResult.sh</p>
<div align=center>
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/terminateTest.jpg"  align=center />
</div>
<p align=center>terminateTest.sh</p>

Interface implementation
------------------------
<p>1. Read and write configuration file</p>
<div>
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/interface3.jpg"  align=center />
</div>
<br />
<div align=center>
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/interface1.jpg"  align=center />
</div>
<br />
<div align=center>
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/interface2.jpg"  align=center />
</div>
<p>2. The directory of configuration files</p>
<p>(1) Data directory</p>
<div>
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/data_catalog.jpg" width = "270" height = "110" align=center />
</div>
<p>(2) bestconf.properties </p>
<div>
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/bestconf_properties.jpg" width = "290" height = "110" align=center />
</div>
<p>(3) defaultConfig.yaml(the parameters need to tune)  </p>
<div>
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/defaultConfig_yaml.jpg"  align=center />
</div>
<p>(4) defaultConfig.yaml_range(the range of parameters) </p>
<div>
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/defaultConfig_yamlrange.jpg"  align=center />
</div>
<p>(5) SUTconfig.properties </p>
<div >
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/SUTconfig_properties.jpg"  align=center />
</div>
<br />
<div>
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/SUTconfig_properties2.jpg" width = "310" height = "210" align=center />
</div>
<br />

Apply and extend BestConfig
---------------------------
1. Apply BestConfig <br />
   (1) Shell scripts <br />
       a. deployed on systems under test <br />
       b. deployed on test node <br />
       <br />
   (2) Directory of configuration files <br />
    a. Parameters(ranges) to be tuned--They can be automatically extracted from system under test <br />
    b. Configuration files related to tuning process and system under test <br />
       <br />
2. Extend BestConfig <br />
   (1) Extended sampling algrithom <br />
       --> Extend the abstract class of ConfigSampler <br />
 <div>
 <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/ConfigSampler1.jpg"  align=center />
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/ConfigSampler2.jpg"  align=center />
 </div>
    <br />
   (2) Extended optimization algrithom <br />
       --> Implement the interface of Optimization <br />
       <div>
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/Optimization1.jpg"  align=center />
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/Optimization2.jpg"  align=center />
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/Optimization3.jpg"  align=center />
    <img src="https://github.com/zhuyuqing/bestconf/blob/master/doc/pics/Optimization5.jpg"  align=center />
    </div>
