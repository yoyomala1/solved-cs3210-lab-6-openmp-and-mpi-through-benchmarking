Download Link: https://assignmentchef.com/product/solved-cs3210-lab-6-openmp-and-mpi-through-benchmarking
<br>
This lab aims to demonstrate the use of benchmarks for performance evaluation of systems. We would be using MPI and OpenMP implementations of Integer Sort (IS) benchmark application from NASA NPB Benchmark Suite for the lab.

NASA NPB Benchmark Suite

The NASA Parallel Benchmarks (NPB) are a small set of programs designed to help evaluate the performance of parallel systems. They were mainly intended for evaluating the performance of supercomputers. The benchmarks are derived from computational fluid dynamics (CFD) applications and have been implemented in many different parallel application paradigms such as OpenMP, MPI and Multi-Zone (hybrid).

<sub></sub> You may find more information and download the benchmark suite at:<a href="https://www.nas.nasa.gov/publications/npb.html">MARKS</a> webpage. <a href="https://www.nas.nasa.gov/publications/npb.html">NAS PARALLEL BENCH-</a>

<h1>Part 1: Integer Sort (IS) Benchmark</h1>

Despite its name, Integer Sort (IS) benchmark included in NASA NPB benchmark suite actually ranks a list of integer values by assigning them a number which indicates its position in the sorted list rather than rearranging their position to compile a sorted list.The benchmark scales by controlling the input size through a compile time parameter from a predefined set of input sizes, namely S, A, B, C and D.

<table width="601">

 <tbody>

  <tr>

   <td width="601">1. Generate N random keys <em>K</em><sub>0</sub><em>,..,K<sub>N</sub></em><sub>−1 </sub>with <em>K<sub>j </sub></em>∈ {0<em>,..,B<sub>max</sub></em>−1} using a random number generator 2. Begin timing3. do for <em>i </em>= 1 <em>to </em>10(a) Modify the sequence of keys:<em>K</em><em>i </em>← <em>i, K</em><em>i</em>+10 ← (<em>B</em><em>max </em>− 1)</td>

  </tr>

 </tbody>

</table>

1

<table width="601">

 <tbody>

  <tr>

   <td width="601">(b)     Ranking:Compute rank: {0<em>,..,N </em>− 1} → {0<em>,..,B<sub>max </sub></em>− 1} so that <em>rank</em>(<em>j</em>) = #{<em>k</em>|<em>K<sub>k </sub>&lt; K<sub>j</sub></em>}.(c)     Partial verification test:Check the value of <em>rank</em><sub>(<em>j</em>) </sub>for a set of specified <em>j </em>∈ {<sub>0<em>,..,N </em></sub>− <sub>1</sub>}. 4. End timing 5. Perform full verification test:Sort the keys according to their rank and verify that <em>K</em><sub>0 </sub>≤ <em><sub>K</sub></em><sub>1 </sub>≤ <em><sub>.. </sub></em>≤ <em><sub>K</sub></em><em><sub>N</sub></em><sub>−1</sub>.</td>

  </tr>

 </tbody>

</table>

For more information on the IS benchmark (and other NPB benchmarks) please refer to this

article: <a href="https://www.davidhbailey.com/dhbpapers/npb.pdf">THE NAS PARALLEL BENCHMARKS</a>

In this lab, we focus on the performance of IS benchmark implemented in three different paradigms; serial implementation, OpenMP shared memory implementation and MPI distributed memory implementation.

<table width="601">

 <tbody>

  <tr>

   <td width="70"></td>

   <td width="531">Please note that there are some known issues with the OpenMP version of the original benchmark suite 3.3.1 version. For this lab, we have adopted a fixed version of OpenMP IS benchmark from <a href="http://aces.snu.ac.kr/software/snu-npb/">SNU NPB Suite</a> from Seoul National University.</td>

  </tr>

 </tbody>

</table>

<h2>Directory Structure</h2>

For the purpose of this lab, we have organized the three versions of IS benchmark in three different directories; SER, OMP, MPI. (SER stands for Serial non-parallel implementation) Inside each of these directories, there are five subdirectories:

<ol>

 <li>IS – contains main source code for IS benchmark</li>

 <li>common – contains utilities such as timers for different systems</li>

 <li>sys – contains utilities used for build process</li>

 <li>config – contains configuration files</li>

 <li>bin – directory where executable binaries would be stored after build process</li>

 <li></li>

 <li></li>

 <li>                                              Main Components in the Source Code</li>

</ol>

As illustrated in the above mentioned pseudocode, there are few main components in the benchmark source code.

<ol>

 <li>Random number generator</li>

 <li>Ranking function</li>

 <li>Verification function</li>

</ol>

<table width="601">

 <tbody>

  <tr>

   <td width="70"></td>

   <td width="531"><strong><u>Exercise 1</u></strong>Download and extract provided lab files archive and observe the directory structure. Navigate to the different implementations’ directories; SER, OMP, MPI and locate the is.c source file inside IS subdirectory. Try to identify the above mentioned main functions in the source code and understand how they work in serial, OpenMP and MPI implementations.</td>

  </tr>

 </tbody>

</table>

<h2>Configuration</h2>

All NPB benchmarks come with a make.def configuration file located inside the config directory. There would be separate configuration files for each implementation type. Usually, you need to make necessary changes such as specifying the relevant compiler and compiler flags in the configuration file in order to properly build the benchmark. The configuration files we have provided you for the lab have been modified to run on lab computers, thus you would not require to do any modifications to build the benchmark.

<table width="601">

 <tbody>

  <tr>

   <td width="70"></td>

   <td width="531"><strong><u>Exercise 2</u></strong>Locate the config folder for each implementation type and try to understand the different configuration options provided in the configuration file make.def. Note that there are two main sections in the configuration file dedicated for Fortran and C. This is because the NPB full suite contains both Fortran and C programs and the config file serves both types.</td>

  </tr>

 </tbody>

</table>

<h2>Compilation/Build and Execution</h2>

NPB benchmarks come with relevant Makefiles to help build the benchmark according to the configuration specified in the make.def file. However, the build command slightly varies across different implementations as shown below. (Make sure that you have a directory named bin under SER, OMP and MPI directories before issuing the make command.)

<h3>Building Serial Version</h3>

Navigate into the SER directory and type in terminal (console):

 &gt; make is CLASS=S

This should generate is.S.x binary in SER/bin directory.

<h3>Building OMP Version</h3>

Navigate into the OMP directory and type in terminal (console):

 &gt; make is CLASS=S

This should generate is.S.x binary in OMP/bin directory.

<h3>Building MPI Version</h3>

Navigate into the MPI directory and type in terminal (console):

 &gt; make is NPROCS=2 CLASS=S

This should generate is.S.2 binary in OMP/bin directory.

In the above make commands, ‘is’ refers to the name of the benchmark, CLASS refers to the input size and NPROCS refers to the number of MPI processes. Note the difference between the OMP and MPI build commands where MPI requires the number of processes along with the input size whereas OMP only requires the input size.

<table width="601">

 <tbody>

  <tr>

   <td width="70"></td>

   <td width="531"><strong>Input Sizes</strong>Information on input sizes/classes are available at <a href="https://www.nas.nasa.gov/publications/npb_problem_sizes.html">NPB Problem Sizes</a> webpage.</td>

  </tr>

 </tbody>

</table>

<h3>Running Serial Version</h3>

Navigate into the SER/bin directory and type in terminal (console):

 &gt; ./is.S.x

This command should start running the serial IS benchmark and the progress would be shown on the screen.

<h3>Running OMP Version</h3>

OMP version require setting the OMP_NUM_THREADS environment variable to specify how many threads we want to run. Recall the OpenMP lab we studied and different ways we could use to specify the number of threads.

Navigate into the OMP/bin directory and type in terminal (console):

&gt; export OMP_NUM_THREADS=2

This would set the number of threads to 2. Then, execute the binary.

&gt; ./is.S.x

This command should start running the OpenMP IS benchmark and the progress would be shown on the screen.

<h3>Running MPI Version</h3>

As we learned in the MPI lab, MPI version of the benchmark could be run on a single node or on a cluster. Recall how we used the machinefile and rankfile to control the execution of MPI programs. Once you decide the configuration, you can issue the command from the MPI/bin directory.

 &gt; mpirun -np 2 is.S.2

This command should start running the MPI IS benchmark on a single node and the progress would be shown on the screen. Please remember to copy the MPI binaries to other nodes when running in cluster.

<table width="601">

 <tbody>

  <tr>

   <td width="70"></td>

   <td width="531"><strong><u>Exercise 3</u></strong>At the moment, there are S,A,B,C and D classes available for IS benchmark. (However there are few known issues reported with class D.) Please refer to the above mentioned resource webpage on NPB problem sizes and explore how the problem size changes from one class to another. Experiment with building executing serial, OMP and MPI versions of IS benchmark for different numbers of threads/processes.</td>

  </tr>

 </tbody>

</table>

<h1>Part 2: Performance Measurement</h1>

<h2>Compare and Contrast Performance of Different Parallel Implementations</h2>

All NPB benchmarks computes a set of performance statistics at the end of execution. At the completion of the execution, this performance statistics report will be displayed on the screen. See below for an example performance statistics report:

NAS Parallel Benchmarks (NPB3.3-OMP) – IS Benchmark

Size: 8388608 (class A) Iterations: 10

Number of available threads: 4

iteration

1

2

3

4

5

6

7

8

9

10

IS Benchmark Completed

Class                                =                                                                A

Size        =              8388608 Iterations              =              10

Time in seconds =               0.26 Total threads               =              4

Avail threads              =                                                                4

Mop/s total                  =                                                    324.14

Mop/s/thread              =                                                       81.04

Operation type = keys ranked Verification     =              SUCCESSFUL

Version                           =                                                       3.3.1

Compile date               =                                        11 Nov 2018

Compile options:

CC                                = gcc

CLINK                          = $(CC)

C_LIB                         = -lm

C_INC                           = -I../common

CFLAGS                                = -g -Wall -O3 -fopenmp -mcmodel=medium

CLINKFLAGS                  = -O3 -fopenmp -mcmodel=medium

This example is for executing the OpenMP version with 4 threads. You can see that there are 10 iterations in the program. Performance statistics include the size, threads, execution time, instruction throughput and whether the verification is successful. These timings do not include the time taken for random number generation and verification step after ranking.

<table width="601">

 <tbody>

  <tr>

   <td width="70"></td>

   <td width="531"><strong><u>Exercise 4</u></strong><strong>Performance Comparison</strong>1.    Build all three versions (SER, OMP, MPI) for C class/problem size.2.    Execute and record performance statistics for SER version.3.    Execute the OMP version (Class C) for different number of threads (2, 4, 8, 16, 32, …) and record the performance statistics.4.    Execute the MPI version (Class C) for different number of processes (2, 4, 8, 16, 32, …) (i) with a cluster of only Corei7 machines and (ii) with a cluster of only Xeon Machines.5.    Compare the performance of each version based on your recorded performance statistics.6.    Compute the speedup.</td>

  </tr>

 </tbody>

</table>

<h2>Verifying the Amdahl’s Law on Scaling</h2>

IS benchmark consist of a non-parallel portion and a parallel portion. We learned in the class that according to Amdahl’s law, the speedup is limited by sequential portion of the application when the number of processes increase.

where <em>f </em>denotes the sequential portion of the application and <em>p </em>denotes the number of processes.

<table width="601">

 <tbody>

  <tr>

   <td width="70"></td>

   <td width="531"><strong><u>Exercise 5</u></strong><strong>Verify Amdahl’s Law</strong>Explain and demonstrate how to compute <em>f </em>(in above expression) based on the measurements.[Hint: you may use Linux time utility to measure the total time].</td>

  </tr>

 </tbody>

</table>


