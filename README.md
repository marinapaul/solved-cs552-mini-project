Download Link: https://assignmentchef.com/product/solved-cs552-mini-project
<br>
<span class="kksr-muted">Rate this product</span>

Detailed configurations of Google cloud instance is as below –

1. Login to GCP using ur personal Gmail account.2. In the compute engine category, Click on VM instances and then click on create instance. 3. I have created an instance with name project-1 under project “My first Project”.

4. Below are the configurations chosen for the instance while creating – 2 VCPU, 4GB RAM and 30GB disk size and Operating System: Ubuntu (18.04 LTS). This instance is considered as native environment.

Steps to enable Docker container are as below –

1.Before installing the docker switched the system login from normal user to root user by using commands,

$sudo su

2.In the next step followed the process documents given to install the Docker CE on the Native OS.

3.Download the sysbench application inside the docker using command

$docker run csminpp/ubuntu-sysbench

The above command pulls the image from the docker registry and ensures it is saved inside docker repository not in native OS.

3. After the installation of Docker, I performed some basic commands like below, and they are as following –

$docker pull – to pull an image from the docker registry on to the system.

$docker run –creates and runs the container$docker ps -a –to list all the containers that we ran along with their status

After the installation was complete, I run the basic “Hello World” program in the container to check if the Docker container is up and running. The output was a success and is as below –

Docker Measurement

Docker is installed and docker container performance is measured using Sysbench Benchmark tool. Docker container image csminpp/ubuntu-sysbench is used to check the system performance.

Below commands are used to use docker container image. Mainly two test modes are performed – cpu test mode and io test mode.

1) CPU Utilization

I performed cpu utilization operation. CPU utilization test enables multiple threads to execute prime number calculation until the command is satisfied (i.e till the maximum prime number mentioned in the command) and gives output the total time taken.

On the basis of my observation and executing the command for several iterations, I decided and selected maximum prime number to be checked as 27000 as the time taken to complete execution was between 30 sec to 50 sec. I performed the above test three times to get the average value.

The command for CPU utilization is as below –

$sysbench –test=cpu-max-prime=27000 run

Also, I performed the iostat test simultaneously and the output is saved in the log files.The command to obtain the user level performance data is as below –iostat -k 2 20 &gt; [output_file name]

whereiostat – iostat is the command used to get user level performance data

-k – is the flag used, similarly we do have [-c], [-d], [-k] and many more flags.

The next parameters 2 and 20, 2 is the time period gap after which the output should calculated and 20 is the number of observations to be found.

Output_file name – output file name is where the output/ performance data should be stored and to store it ‘&gt;’ operator is used.

The output of first test mode is as below –

User level performance data is calculated by using the command –

iostat -k 2 20 &gt; output file_name

$docker pull – to pull an image form the docker registry on to the system. $docker run –creates and runs the container$docker ps -a –to list all the containers that we ran along with their status

To come out of the docker container and to the native OS terminal I simply used the command$exit

Analysis of the CPU Test Mode data is as below –

Above is the bar graph representing total time taken to run the CPU test mode. From the graph, it is visible that the total time taken is increasing exponentially.

2) File I/O

The File I/O test mode is used to generate various kinds of file I/O workloads. There are three stages of this test mode – prepare, run and cleanup.A) Prepare stage –

In this stage, sysbench creates a specified number of files with a specified total size.Below is the command for the prepare stage –sysbench –test=fileio –file-total-size=1G prepare

<ol start="2">

 <li>B)  Run stage –In this stage, each thread performs specified Input/Output operations on the set of files mentioned in prepare stage.Below is the syntax/command for the run stage –sysbench -test=fileio -file-total-size=1G –file-test-mode=rndrw –max-time=60 –max-requests=0 run</li>

 <li>C)  Cleanup stage –In this stage, the files used for the test are removed. For example –</li>

</ol>

sysbench –num-threads=12 –test=fileio –file-total-size=3G –file-test- mode=rndrw prepare

This command creates 128 files with the total size of 3 GB in the current directory.

The parameters are as below –Num-threads -&gt; Number of threads/files to be createdFile-total-size -&gt; Size of each file to be createdFile-test-mode -&gt; test mode specifys the I/O operations to be supported.

Below are the different I/O operations supported –

<ol>

 <li>1)  seqwr – sequential write</li>

 <li>2)  seqrewr – sequential rewrite</li>

 <li>3)  seqrd – sequential read</li>

 <li>4)  rndrd – random read</li>

 <li>5)  rndwr – random write</li>

 <li>6)  rndrw – combined random read/write</li>

</ol>

$ sysbench –num-threads=12 –test=fileio –file-total-size=3G –file-test- mode=rndrw runThis command will run the actual benchmark and displays the results upon completion.

$ sysbench –num-threads=12 –test=fileio –file-total-size=3G –file-test- mode=rndrw cleanupThis command will remove the files used for the test.

After installation of docker, I performed the file I/O test inside docker using the below commands –sysbench ––test=fileio –file-total-size=1G preparewhere,

file-total-size -&gt; is size of which files should be created

sysbench – -test=fileio –file-total-size=1G – -file-test-mode=rndrw – -max-time=60 – -max-requests=0 runwhere,file-total-size -&gt; is size of which files should be created

file-test-mode -&gt; the type of work load to be created, here it is rndrw which is random read and write.

max-time -&gt; Maximum time for which the test should be running, here it is 60 seconds.

Max-requests -&gt; limit the total number of requests.

sysbench – -test=fileio –file-total-size=1G – -file-test-mode=rndrw – -max-time=60 – -max-requests=0 cleanup

After performing, these 3 commands, I came outside the docker container using command exit.In the native environment, I logged in as the root user and cleared the cache using the below command –

echo 3 &gt; /proc/sys/vm/drop_caches

While executing the file I/O test mode, I have collected the CPU performance (user level and kernel level), disk utilization and I/O performance of native environment using iostat tool.

Below are the commands for the same –

$iostat ALL -t 90 20

This command displays the cpu utilization by kernel level (i.e CPU usage of operating system), user level (i.e CPU usage of user), nice (i.e amount of time a low priority process have used the cpu) and cpu idle time.

$iostat -xd -t 90 20

This command displays detailed information like tps (transfers per second), read &amp; write per second, I/O latency (await time), rrqm/sec, wrqm/s (read and write request queued for the I/O scheduler per second) and much more.

$df -h

This command displays the disk utilization of file system. Following are the results of File I/O test mode –

Similarly, I performed this step two more times. The commands and their result are as following –

Analysis of data is as below –

The total time taken by the sysbench benchmark to run the I/O test mode is plotted as a bar graph. As we can see, the total time taken to run the benchmark is increasing exponentially.

QEMU Based VM

I installed QEMU as per the steps given in the document and reference. The complete installation took 2 to 3 hours.

Below are the reasons why QEMU based VM so slow to install and execute.

<ol>

 <li>1)  QEMU based VM requires various number of libraries to be installed for thecompletion of the installation. Thus, installation of QEMU based VM is very time consuming.</li>

 <li>2)  QEMU ignores the presence of hardware virtualization capabilities. Depending on the target architecture, “tcg” is made available where tcg is Tiny Code Generator. Tiny Code Generator slowly emulates the guest CPU in software.</li>

 <li>3)  QEMU based VM needs a GUI and it occupies a large amount of disk space. So it is slower to install.</li>

</ol>

<ol start="4">

 <li>4)  There can a network connectivity issue as we are installing the VM on Google Cloud Platform via a local server.</li>

 <li>5)  During the booting process, QEMU based VM has to load all the libraries &amp; dependencies and also GUI.</li>

 <li>6)  QEMU is very complex and thus has very slow functioning.</li>

</ol>