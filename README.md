[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)

# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: LIU, Yishan

### Student Id: 21086382

### Email: yliuoj@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose _any_ open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

   > **Phoronix Test Suite** is used to measure the CPU and memory performance.
   >
   > To measure CPU performance, we ran the 'pts/compress-7zip' test and picked the compression rating, since compression task is CPU-intensive.
   >
   > To measure memory performance, we ran the 'pts/ramspeed' test (type=average, benchmark=integer). This simply measures the memory bandwidth in various scenarios.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

   In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

   | Size        | CPU performance | Memory performance |
   | ----------- | --------------- | ------------------ |
   | `t2.micro`  | 3455 MIPS       | 10355.92 MB/s      |
   | `t2.medium` | 9620 MIPS       | 18482.8 MB/s       |
   | `c5d.large` | 7626 MIPS       | 13414.76 MB/s      |

   > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

   | Type                      | TCP b/w (Mbps) | RTT (ms) |
   | ------------------------- | -------------- | -------- |
   | `t3.medium` - `t3.medium` | 4480           | 0.252    |
   | `m5.large` - `m5.large`   | 4970           | 0.274    |
   | `c5n.large` - `c5n.large` | 4970           | 0.131    |
   | `t3.medium` - `c5n.large` | 4700           | 0.213    |
   | `m5.large` - `c5n.large`  | 4970           | 0.193    |
   | `m5.large` - `t3.medium`  | 4590           | 0.219    |

   > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

   | Connection                | TCP b/w (Mbps) | RTT (ms) |
   | ------------------------- | -------------- | -------- |
   | N. Virginia - Oregon      | 470            | 59.610   |
   | N. Virginia - N. Virginia | 4640           | 0.346    |
   | Oregon - Oregon           | 4760           | 0.202    |

   > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
