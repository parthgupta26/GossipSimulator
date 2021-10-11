# COP5615 Distributed Operating System Principles Project 2

## Gossip-Simulator-Actor-Model-F#-Akka.Net

## Project Description

The goal of this project is to determine the convergence time of gossip ans push-sum algorithms through a simulator based on actors written in F#. The Gossip type algorithms can be used both for group communication and for aggregate computation. Since actors in F# are fully asynchronous, the particular type of Gossip implemented is the so called Asynchronous Gossip. 

### Gossip  Algorithm  for  information  propagation

#### Starting:

A participant (actor) is told to sent a roumor (message) by the mainprocess.

#### Step:

Each actor selects a random neighbor and tells it the rumor.

#### Termination:

Each actor keeps track of rumors and how many times it has heard the rumor. It stops transmitting once it has heard the rumor n times. n can be any number.

### Push-Sum algorithm for sum computation

#### State:

Each actor maintains two quantities:s and w. Initially, s = xi = i (that is actor number i has value i, play with other distribution if you so desire) and w = 1.

#### Starting:

Ask one of the actors to start from the main process.

#### Receive:

Messages sent and received are pairs of the form (s, w). Uponreceive, an actor should add received pair to its own corresponding values.  Upon receive, each actor selects a random neighbor and sends it a message.

#### Send:

When sending a message to another actor, half of s and w is kept by the sending actor and half is placed in the message.

#### Sum estimate: 

At any given moment of time, the sum estimate is s/w where s and w are the current values of an actor. 

##### Termination:

If an actors ratio s/w did not change more than 10^(-10) in 3 consecutive rounds then the actor terminates. WARNING: the values s and w independently never converge, only the ratio does.

### Topologies

The actual network topology plays a critical role in the dissemination speed of Gossip protocols. The topology determines who is considered a neighboor in the above algorithms.

#### Line

Actors are arranged in a line. Each actor has only 2 neighbors (one left and one right, unless you are the first or last actor).

#### Full

Every actor is a neighbor of all other actors except itself. That is, every actor can talk directly to any other actor.

#### 3D

Actors form a 2D grid. The actors can only talk to the grid neighbors.

#### Imperfect 3D

Grid arrangement but one random other neighbor is selected from the list of all actors (6 + 1 neighbors).

## Project Requirements

### Input

The input provided (as command line) will be of the form: numOfNodes topology algorithm Where numOfNodes is the number of actors involved , topology is one of line, full, 3D, imp3D, algorithm is one of gossip, and push-sum.

### Output

Print the amount of time (in milliseconds) it took to achieve convergence of the algorithm.  

### Example:

dotnet fsi Project2.fsx 10000 line gossip <br>
Time to converge : 6462.665300

## Submitted By:

Name: Parth Gupta, UFID: 91997064

## What is Working?

- Convergence for Gossip Algorithm for all Topologies (Line, Full, 3D, imp3D).
- Convergence for Push Sum Algorithm for all Topologies (Line, Full, 3D, imp3D).

## The largest network that I managed to deal with for each type of topology and algorithm

| Topology / Algorithm | Gossip | Push Sum |
| --- | --- | --- |
| Line | 30000 | 1500 |
| Full | 30000 | 22500 |
| 3D | 60000 | 2000 | 
| imp3D | 60000 | 10000 |

## Built On

- Programming language: F# 
- Framework: AKKA.NET
- Operating System: Windows 10
- Programming Tool: Visual Studio Code
