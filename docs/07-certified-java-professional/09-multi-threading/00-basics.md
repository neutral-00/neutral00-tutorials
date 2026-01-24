# Core Concepts


## Credit
1. Youtube Tutorial by `@EngineeringDigest`


## CPU
- stands for Central Processing Unit. It is known as the brain of the computer.
- It executes instructions from programs.
- It can execute arithmetic, logic, control and input output operations.
- Majority of the CPUs are developed by Intel or AMD like Intel i7, amd Ryzen 7.

## Core
- It is an individual processing unit of a CPU.
- A CPU nowadays have multiple cores.
- Intel Core i7 typically has 4 to 24 cores depending on the generation.
- 14th Gen Intel Core i7 can have 20 cores.

**NOTE**
- To know the number of cores type `wmic cpu get NumberOfCores`
- To know the number of logical processors type `wmic cpu get NumberOfLogicalProcessors`
- I have 8 cores(physical processors) 
- but using Intel's hyperthreading technology some of these cores can handle multiple threads by sharing resources.
- If hyperthreading is enabled, and a core supports it, then 1 core can handle 2 threads simultaneously.
- Looks like two of my core supports it. So I got 12 logical processors in my system.
- My Operating System sees 12 processing units


## Program
- It is a set of instructions written in a programming language.
- The instructions tell the computer to perform some tasks.
- For example Chrome browser is a program using which you can browse the internet.

## Process
- Process is an instance of a instance of a program.
- When a program is started, OS creates a process to manage its execution.
- When 2 times chrome is opened, 2 windows created and OS creates 2 process.

## Threads
- A thread is the smallest unit of execution within a process.
- A process usually has multiple threads.
- Threads run independently and share the same resources.

## Multitasking
- OS can run multiple processes simultaneously on a single core.
- This is achieved through time sharing and rapidly switching bewteen tasks.
- This is called multitasking.
- On a multi-core cpu, true parallel execution occurs. Tasks are distributed across cores.
- This is done by OS scheduler.


## Multithreading
- refers to the ability to execute multiple threads within a single progess concurrently.
- it enhances the efficiency of multitasking by breaking down individual process into threads.

**NOTE**
- In single core cpu, threads and processes are manage by the scheduler through time slicing and context switching.
- This creates an illusion of simultaneous execution.
- But in multi-core cpu, both threads and processes run in different cores parellelly.

## Time Slicing
- CPU time is divided into small intervals called time slices or quanta.
- The schedule allocates these time slices to different processes and threads.

## Context Switching
- It is the process of saving the state of the current thread then loading the state of the next thread.

## Summary
- Multitasking typically refers to the running of multiple applications.
- Multithreading is more granular and refers to the executions of multiple threads of a process.
- Multitasking is achieved through multithreading.

