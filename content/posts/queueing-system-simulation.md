---
date: '2024-10-20T20:00:32+08:00'
draft: true
title: 'Queueing System Simulation'
---

# Grocery Stores

## Simulation of Queueing Systems

A queueing system is characterized by the following elements:

- Calling Population: Potential customers who may enter the system.
- Arrival Rate: Frequency of customer arrivals (inter-arrival times).
- Service Mechanism: How services are provided (number of servers and speed).
- System Capacity: Maximum number of customers allowed in the system.
- Queueing Discipline: Order in which customers are served (e.g., FIFO - First In, First Out).

## Example

- Analysis of a small grocery store

  - One checkout counter
  - Customers arrive at random times from {1,2,...,8}
  - Service times vary from {1,2,...,6}
  - Consider the system for 100 customers

- Problems/Simplifications

  - Sample size is too small to be able to draw reliable conclusions
  - Initial condition is not considered

- Interesting results for a manager, but

  - longer simulation run would increase the accuracy

- Some interpretations
  - Average waiting time is not high
  - Server has not undue amount of idle time, it is well loaded
  - Nearly half of the customers have to wait

## Final Exam Question (May 2018)

A queuing system in a minimarket occur randomly with inter-arrival time {1..6} and service time {1..10}. The following table Q1 depicts results of the simulation towards five regular customers.

| Customer No | Customer Name | Inter-arrival time | Arrival Time on clock | Service time |
| :---------: | :-----------: | :----------------: | :-------------------: | :----------: |
|      1      |     Bobby     |         -          |           0           |      10      |
|      2      |     Lucy      |         5          |           5           |      8       |
|      3      |     Anie      |         2          |           7           |      9       |
|      4      |     Diana     |         1          |           8           |      5       |
|      5      |    Stewart    |         2          |          10           |      2       |

Analyze the simulation results and answer the following questions with appropriate explanation:

> Find ONE(1) potential complain that may arise from the above simulation. What is the best way to avoid this complain?

ss

> Were Bobby and Lucy queuing before approaching cashier? What could be the reason?

> How long the cashier were idle in between services? Will it affect the business?

The cashier were not idle in between services.

> Assume Diana is a customer who uses a wheelchairand she comes alone. Should she deserve a special assistance while queuing? Discuss your answer.

| Customer  | Interarrival Time | Arrival Time | Service Time | Time Service Begins | Time Service Ends | Waiting Time in Queue | Time Customer in System | Idle Time of Server |
| :-------: | :---------------: | :----------: | :----------: | :-----------------: | :---------------: | :-------------------: | :---------------------: | :-----------------: |
|     1     |         0         |      0       |      10      |          0          |        10         |           0           |           10            |          0          |
|     2     |         5         |      5       |      8       |         10          |        18         |           5           |           13            |          0          |
|     3     |         2         |      7       |      9       |         18          |        27         |          11           |           20            |          0          |
|     4     |         1         |      8       |      5       |         27          |        32         |          19           |           24            |          0          |
|     5     |         2         |      10      |      2       |         32          |        34         |          22           |           24            |          0          |
| **Total** |        10         |              |      34      |                     |                   |          57           |           91            |          0          |

# Call Centers

- Consider a Call Center where technical personnel take calls and provide service
- Two technical support people (2 server) exists
  - Able - more experienced, provides service **faster**
  - Baker - provides service **slower**
- Rule
  - Able gets call if both people are idle
  - Try other rules
    - Baker gets call if both are idle
    - Call is assigned randomly to Able and Baker
- Goal of study: Find out how well the current rule works

- Interarrival distribution of calls for technical support

- Simulation run for 100 calls

![](http://s1.wailian.download/2020/04/23/image.png)

## Tutorial

Inter-Arrival Time (I) and Service Time (S) is depicted as {I,S} below.
{0,3}
{2,4}
{3,2}
{2,5}
{2,2}
{3,3}

> Identify how many calls completed by Able and Baker, caller delay and time in the system for the above arrivals.

| Caller Nr. | Interarrival Time | Arrival Time | When Able Avail. | When Baker Avail. | Server Chosen | Service Time | Time Service Begins | Able's Service Compl. Time | Baker's Service Compl. Time | Caller Delay | Time in System |
| ---------- | ----------------- | ------------ | ---------------- | ----------------- | ------------- | ------------ | ------------------- | -------------------------- | --------------------------- | ------------ | -------------- |
| 1          | \-                | 0            | 0                | 0                 | Able          | 3            | 0                   | 3                          |                             | 0            | 3              |
| 2          | 2                 | 2            | 3                | 2                 | Baker         | 4            | 2                   |                            | 6                           | 0            | 4              |
| 3          | 3                 | 5            | 5                | 6                 | Able          | 2            | 5                   | 7                          |                             | 0            | 2              |
| 4          | 2                 | 7            | 7                | 7                 | Able          | 5            | 7                   | 12                         |                             | 0            | 5              |
| 5          | 2                 | 9            | 12               | 9                 | Baker         | 2            | 9                   |                            | 11                          | 0            | 2              |
| 6          | 3                 | 12           | 12               | 11                | Able          | 3            | 12                  | 15                         |                             | 0            | 3              |
| Total      |                   |              |                  |                   |               |              |                     |                            |                             | 0            | 19             |

# Inventory System

- Distributes items from current inventory to customers
- Customer demand is discrete
- Simple <-> one type of item

## Final Exam Question

### Question 1

An inventory system is doing a periodic inventory review and simulation to ensure the flow is balanced between stock and demand. Let (s,S) = (25,65) where s is the minimum inventory level and S is the maximum inventory level.

> Discuss FIVE(5) inventory system costs that affect the performance of an inventory system.

- Holding cost
  for items in inventory
- Shortage cost
  for unmet demand
- Setup cost
  fixed cost when order is placed
- Item cost
  per-item order cost
- Ordering cost
  sum of setup and items costs

> Assume n = 10 for the time intervals and the value of i (inventory level) and di (demand quantity during the interval) is given by the following table.

| _i_  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8  |  9  | 10  |
| :--: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| _di_ | 40  | 25  | 35  | 25  | 55  | 40  | 35  | 25  | 30  | 45  |

> With the aid of the diagram, find any _shortage_ that occurs in the system during the interval. Should the inventory level (s,S) be modified based on this periodic review? Explain your answer.

# Poisson Distribution

- A Poisson distribution helps in describing the chances
  of occurrence of a number of events in some given time interval that the value of average number of
  occurrence of the event is known.
- This is a major and only condition of Poisson distribution.
- An experiment in statistics is termed as Poisson experiment when it possesses the following probabilities:
  - The outcomes of the experiment can be easily classified as either success or failure.
  - The average of the number of successes within a region that is specified is known.
  - The probability of occurrence of a success is always proportional to the size of the specified region.
  - The probability of occurrence of success in a very small region is zero virtually.
  - It is to be noted that the region that is specified can take different forms like area, length, time period etc

> **Predict future occurences based on history**
> Step 1 - get &#x03BB (history of things occured)
> Step 2 - get table of &#x03BB (poisson distribution)
> Step 3 - project probability numbers ~ exact value ~ range of numbers

## Example

|  x  | &#x03BB | P(_x_) for &#x03BB = 3 |
| :-: | :-----: | :--------------------: |
|  0  |    3    |        0.04979         |
|  1  |    3    |        0.14936         |
|  2  |    3    |        0.22404         |
|  3  |    3    |        0.22404         |
|  4  |    3    |        0.16803         |
|  5  |    3    |        0.10082         |
|  6  |    3    |        0.05041         |
|  7  |    3    |        0.02160         |
|  8  |    3    |        0.00810         |
|  9  |    3    |        0.00270         |
| 10  |    3    |        0.00081         |
| 11  |    3    |        0.00022         |
| 12  |    3    |        0.00006         |
| 13  |    3    |        0.00001         |
| 14  |    3    |        0.00000         |
| 15  |    3    |        0.00000         |

> 1. A man was able to complete 3 files a day on an average. Find the probability that he can complete 5 files the next day. _Hint: find the number on the table._

P(X = 5) = 0.00757

> 2. The number of calls coming per minute into a hotels reservation center is Poisson random variable with mean. Find the probability that no calls come in a given 1 minute period. _Hint: find the probability number on the table._

P(X = 0) = 0.00005

> 3. Let X equal the number of typos on a printed page with a mean of 3 typos per page. What is the probability that a randomly selected page has at least one typo on it? _Hint: P(X ≥ 1) = 1 − P(X = 0)_

P(X ≥ 1) = 1 − P(X = 0) = 1 - 0.00005 = 0.99995

# Monte Carlo Simulation

> **Predict future achievement of a company based on random numbers**
> Step 1 - relative frequency table
> Step 2 - range of distribution
> Step 3 - random numbers are projected to the range of distribution
> Step 4 - Calculate the company revenue