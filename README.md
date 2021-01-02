# Travelling Salesman Problem with Aanealing algorithm




---

## Description

---

## the traveling salesman problem 

![TSP](https://www.researchgate.net/profile/Israel_Agbehadji2/publication/301325477/figure/fig3/AS:667721079484426@1536208519369/Traveling-Salesman-Problem.png)

The travelling salesman problem (also called the traveling salesperson problem or TSP) asks the following question: "Given a list of cities and the distances between each pair of cities, what is the shortest possible route that visits each city exactly once and returns to the origin city?" It is an NP-hard problem in combinatorial optimization, important in theoretical computer science and operations research.

The travelling purchaser problem and the vehicle routing problem are both generalizations of TSP.

In the theory of computational complexity, the decision version of the TSP (where given a length L, the task is to decide whether the graph has a tour of at most L) belongs to the class of NP-complete problems. Thus, it is possible that the worst-case running time for any algorithm for the TSP increases superpolynomially (but no more than exponentially) with the number of cities.

The problem was first formulated in 1930 and is one of the most intensively studied problems in optimization. It is used as a benchmark for many optimization methods. Even though the problem is computationally difficult, many heuristics and exact algorithms are known, so that some instances with tens of thousands of cities can be solved completely and even problems with millions of cities can be approximated within a small fraction of 1%.

The TSP has several applications even in its purest formulation, such as planning, logistics, and the manufacture of microchips. Slightly modified, it appears as a sub-problem in many areas, such as DNA sequencing. In these applications, the concept city represents, for example, customers, soldering points, or DNA fragments, and the concept distance represents travelling times or cost, or a similarity measure between DNA fragments. The TSP also appears in astronomy, as astronomers observing many sources will want to minimize the time spent moving the telescope between the sources; in such problems, the TSP can be imbedded inside an optimal control problem. In many applications, additional constraints such as limited resources or time windows may be imposed.


## Simulated annealing


Simulated annealing (SA) is a probabilistic technique for approximating the global optimum of a given function. Specifically, it is a metaheuristic to approximate global optimization in a large search space for an optimization problem. It is often used when the search space is discrete (e.g., the traveling salesman problem). For problems where finding an approximate global optimum is more important than finding a precise local optimum in a fixed amount of time, simulated annealing may be preferable to exact algorithms such as gradient descent, Branch and Bound.

The name of the algorithm comes from annealing in metallurgy, a technique involving heating and controlled cooling of a material to increase the size of its crystals and reduce their defects. Both are attributes of the material that depend on their thermodynamic free energy. Heating and cooling the material affects both the temperature and the thermodynamic free energy or Gibbs energy. Simulated annealing can be used for very hard computational optimization problems where exact algorithms fail; even though it usually achieves an approximate solution to the global minimum, it could be enough for many practical problems.

The problems solved by SA are currently formulated by an objective function of many variables, subject to several constraints. In practice, the constraint can be penalized as part of the objective function.

Similar techniques have been independently introduced on several occasions, including Pincus (1970), Khachaturyan et al (1979, 1981), Kirkpatrick, Gelatt and Vecchi (1983), and Cerny (1985). In 1983, this approach was used by Kirkpatrick, Gelatt Jr., Vecchi, for a solution of the traveling salesman problem. They also proposed its current name, simulated annealing.

This notion of slow cooling implemented in the simulated annealing algorithm is interpreted as a slow decrease in the probability of accepting worse solutions as the solution space is explored. Accepting worse solutions allows for a more extensive search for the global optimal solution. In general, simulated annealing algorithms work as follows. The temperature progressively decreases from an initial positive value to zero. At each time step, the algorithm randomly selects a solution close to the current one, measures its quality, and moves to it according to the temperature-dependent probabilities of selecting better or worse solutions, which during the search respectively remain at 1 (or positive) and decrease towards zero. 
The simulation can be performed either by a solution of kinetic equations for density functions or by using the stochastic sampling method. The method is an adaptation of the Metropolis–Hastings algorithm, a Monte Carlo method to generate sample states of a thermodynamic system, published by N. Metropolis et al. in 1953.


---

## Table of Contents 

- [Features](#features)
- [Documentation](#documentation)
- [Support](#support)


---

## Libraries

- #include<stdio.h>
- #include<stdlib.h>
- #include<math.h>
- #include<time.h>
- #include <sys/time.h>
- #include <mpi.h>
- #include <string.h>

---

## MPI Command

- MPI_Init(NULL,NULL); 
- MPI_Comm_rank(MPI_COMM_WORLD,&my_rank); 
- MPI_Comm_size(MPI_COMM_WORLD,&comm_sz);.
- MPI_Barrier(MPI_COMM_WORLD);
- MPI_Reduce(&local_len,&len,1,MPI_DOUBLE,MPI_MIN,0,MPI_COMM_WORLD); 
- MPI_Bcast(&d_len,1,MPI_DOUBLE,0,MPI_COMM_WORLD);
- MPI_Gather(local_i,point_number,MPI_INT,buf,point_number,MPI_INT,0,MPI_COMM_WORLD); 
- MPI_Finalize();

---

## Connect to n-node

`ssh compute-0-n`

--- 

## Building

- **sequential** : ` gcc tsp_sequential.c -o tsp_sequential -std=gnu99 -lm `
- **parallel** : ` mpicc -o tsp_MPI tsp_MPI.c -lm `

---

---

## Running

- **sequential** : `./tsp_sequential`
- **parallel** : `mpirun -np 64 ./tsp_MPI`

---

--- 

## Running Options

### Machine File
- **parallel with machine file** : `mpirun -np 128 -machinefile machine_file_0123.txt ./tsp_MPI`

### Networking
- **TCP/IP over Ethernet**  : `mpirun --mca btl self,tcp --mca btl_tcp_if_include em2 [args] ./myexec`
- **TCP/IP over Infiniband**  : `mpirun --mca btl self,tcp --mca btl_tcp_if_include ib0 [args] ./myexec`
- **Native Infiniband**  : `mpirun --mca btl self,openib [args] ./myexec`

### MPE
- **Generate .clog2**  : `mpecc -mpilog -lpthread –o myexec mysrc.c mpirun [args] ./myexec`
- **Vievwer .slog** : `https://www.mcs.anl.gov/research/projects/perfvis/software/viewers/index.htm`


---

## Features

---

## Execution environment for MPI  (Front-end + 4 nodi computazionali)


> **Front-end** : 
- 2 x Xeon (2.00 GHz)
- Memory (RAM) 8 GB
- Disk da 512 GB

> **Computational node** : 
- 2 processori Xeon (3.40 GHz)
- 8 core fisici a processore
- 16 core per ogni macchina in totale
- Memoria (RAM) 64 GB
- Disco da 1 TB
- Su alcuni nodi è abilitato l’Hyper-Threading

> **OS:** Rocks 7.0 (Manzanita) x86_64 is based upon CentOS 7.4 with all updates available as of 1 Dec 2017.
data avaible at: `http://www.rocksclusters.org/downloads/2017-12-01-download-rocks-7-0-manzanita.html  `

> **Networking:**
- Fast Ethernet -100 Mb/s
- InfiniBand - 56 Gb/sec
---

## Support

- Email at `girolamo.musto@gmail.com`</a>
- Email at `melillo.pietro@gmail.com`</a>

---




