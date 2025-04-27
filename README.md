# cs2106-lab-3-synchronization-mechanisms-solved
**TO GET THIS SOLUTION VISIT:** [CS2106 Lab 3-Synchronization Mechanisms Solved](https://www.ankitcodinghub.com/product/cs2106-introduction-to-operating-systems-solved-3/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;121438&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;1&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (1 vote)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CS2106 Lab 3-Synchronization Mechanisms Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (1 vote)    </div>
    </div>
&nbsp;

1. Introduction

In this lab we will look at synchronization mechanisms to help parallel programs operate correctly. In the first part we will look at the idea of lock variables, and of how to use semaphores. In the second part we will implement barriers using semaphores, and in the third part we will use barriers to help find the smallest and largest elements of a moderately sized array.

As an added challenge we will be using the synchronization mechanisms with processes rather than threads, and we will see how to correctly share mechanisms like semaphores between processes.

a. You can do this lab alone or with a partner. Your partner can be from any lab group.

b. Ensure that both of you fill in your names, student IDs and group numbers in the answer book AxxxxxxY.docx.

c. Rename AxxxxxxY.docx to the student ID of the submitter before submitting.

d. Zip up the following files into a single ZIP file called AxxxxxxY.zip, where AxxxxxxY is your student ID:

– Your answer book, properly renamed.

– Your barrier.c and barrier.h from part 2.

– Your bigsmall-par.c from part 3.

There is no need to submit your codes from part 1.

2. Activities

Part 1. Using Lock Variables and Semaphores

All files needed for this part can be found in the part1 directory. In this part we will look at two ways to do synchronization: Lock variables and semaphores. We begin by opening up lab3p1.c:

This is a simple program that spawns 5 processes, which tries to produce the following output:

We compile and run the program using:

gcc lab3p1.c –o lab3p1

./lab3p1

We see an output similar to this:

Question 1.1 (1 mark)

Explain why all the “&lt;some number&gt; I am child X” (X is some number from 0 to 4) appears before most of the numbers. What does this suggest about the time quantum?

a. Using Lock Variables

We will now explore a mechanism called “lock variables” to try to synchronize the different processes. Lock variables are very simple, and the algorithm below illustrates how they work:

1. Create a new shared variable “lock”. Set it to 1 2. Spawn all processes

3. For each process:

3.1 if lock is 0, goto 3.1 (Busy wait until lock is 1)

3.2 Set lock to 0 (Note: we can only get here when lock is 1 and the loop at 3.1 exits)

3.2 Execute my statements (Note: we can only get here once lock is 1

Part of the code for lab3p1-lock.c is shown below, with the relevant lock code circled:

Note that while the lock variable doesn’t control which process gets to run first. All we want at this point is to get it to do something like the following:

I am child 0

0 1 2 3 4 5 6 7 8 9

I am child 3

31 32 33 34 35 36 37 38 39 etc.

That is, we want one process to complete running before the next one starts.

Compile and run lab3p1-lock.c by using:

gcc lab3p1-lock.c –o lab3p1lock

./lab3p1lock

Question 1.2 (1 mark)

If we look at the result of our program, it’s clear we have not achieved our objective. Explain why the lock variable failed to coordinate the processes.

b. Using Turn Variables

You’ve already seen the concept of “turn variables” in Tutorial 4 Question 4. To summarize:

1. Create a shared variable called “turn”. Set turn to 0.

2. For each process i from 0 to n-1:

2.1 while(turn != i); // Do nothing while it’s not our turn.

2.2 Now it is my turn. Execute my code.

2.3 turn = turn + 1; // Pass turn to next process

You are given a file called lab3p1-shm.c. Modify this program to implement turn variables.

Question 1.3 (1 mark)

c. Using Semaphores

We will now attempt to use semaphores. Open sema-wrong.c (yes, the solution is indeed wrong) and you will see a straightforward but naive attempt to use semaphores to coordinate between processes:

gcc sema-wrong.c –o sema-wrong –lpthread

./sema-wrong

(Note: The –lpthread is important to bring in the semaphore library)

Question 1.4 (1 mark)

Explain each parameter of sem_init, and what sem_wait and sem_post do. Note: If you just say “sem_wait” waits for a semaphore and “sem_post” posts to a semaphore, you will not receive any credit. Your answer must show understanding of what semaphores are and how they work.

Question 1.5 (1 mark)

There is no shared memory between the parent and child process. Explain why this causes the program to hang.

We will now see how to correctly share semaphores between processes. Open sema-right.c and you will see:

a. Our semaphore sem is of type sem_t * instead of sem_t.

b. We create a segment of shared memory using shmget of size sem_t.

c. We attach the shared memory to sem using shmat.

d. From then on we treat sem as an ordinary semaphore. Note that now we pass in sem instead of &amp;sem to sem_wait and sem_post, since sem is now of type sem_t * instead of sem_t.

e. We destroy the semaphore, then detach and release the shared memory once it’s no longer needed.

We compile and run as usual:

gcc sema-right.c –o sema-right –lpthread

./sema-right

We now see that the program runs correctly; the parent pauses for a second before releasing the child and we see:

You are now given lab3p1-sem.c, which at this time is identical to lab3p1.c. Using what you’ve learnt about semaphores, modify lab3p1-sem.c to produce this output, with the correct ordering of processes from 0 to 4 (Hint: Create an array of semaphores):

Question 1.6 (1 mark)

Briefly explain how your program synchronizes the processes to produce the output above. There is no need to cut-and-paste code.

Part 2. Creating Barriers with Semaphores

In this part we will create a barrier using semaphores. Recall that a barrier is a structure that is called by an expected number of processes. All processes except the last will block at the barrier, until the last process calls the barrier, after which all processes are released. All files needed can be found in the part2 directory.

When we create barriers using semaphores, we are relying on the following property of semaphores:

1. We start with sem=0

2. If n processes call wait(sem), all n processes will block.

3. If another process calls signal(sem), ONE of the n processes will be picked to unblock.

4. If each of the n processes also calls signal(sem) after being unblocked, eventually everyone will be unblocked.

Using the principle above, we can design out barrier using the following pseudo-code (note: This is incomplete and just gives you an idea of what to do):

You are given three files barrier.c, barrier.h and test_barrier.c. The barrier.c file contains three functions:

init_barrier: Takes one argument – The number of processes that will call the barrier. This function should create any shared memory required, as well as the semaphores you need. Note that in the algorithm above count is a shared variable that is updated by multiple processes and can thus create race conditions. You will need one more semaphore to act as a mutex to protect this variable.

reach_barrier: Does not take any arguments. Follows the algorithm above.

destroy_barrier: If the caller is a parent process, destroy all semaphores and detach and release all shared memory.

The barrier.h file contains prototypes for barrier.c, and test_barrier.c contains a test program that basically creates 6 children that will sleep a random amount of time of up to 1 second, then call reach_barrier. When all children reach the barrier, the parent will print “All the children have returned.” and exit.

The children too will output “Child X has slept for Y seconds and has now reached the barrier”.

After completing your barrier.c, you can compile and run using:

gcc barrier.c test_barrier.c –o test_barrier –lpthread

./test_barrier

If your barrier works correctly, you should see an output similar to this (sleep times will differ):

Cut and paste your code for init_barrier and explain it.

Question 2.2 (1 mark)

Cut and paste your code for reach_barrier and explain it.

Part 3. Finding Largest and Smallest Element in Parallel

In this part we will search through a moderately sized 2,000,000 element array to find the largest and smallest elements. You are given two programs. Both generate the same 2,000,000 element array of pseudo-random numbers with the same starting seed. Most of what you need can be found in the part3 directory, although you will need to copy over the barrier.* files from the previous part to complete your program.

a. The sequential version bigsmall.c. Compile and run this program:

gcc bigsmall.c -o bigsmall

./bigsmall

You will see:

The random number generator is seeded to 24601, so this program will always produce the same smallest and largest elements. This helps you to check if your program is working correctly.

b. The (incorrectly implemented) parallel version, bigsmall-par.c. This program splits the 2,000,000 element array between 8 processes (250,000 integers per process). There are two arrays “largest” and “smallest” where each process will store its results (e.g. process 1 will store to largest[1] and smallest[1], etc.). The parent is supposed to wait for all child processes to finish before looking through “largest” and “smallest” to find the largest and smallest integers amongst all those found by the children, and print those out.

Compile and execute using:

gcc bigsmall-par.c

./bigsmall-par.c

You will see the following output:

The random number generator is again seeded to 24601, so this output is clearly incorrect.

Now modify bigsmall-par.c to produce the correct answer, subject to the following rules:

a. The program will still distribute the search between 8 processors.

b. You must use barriers to coordinate. No credit will be given if you do not use barriers to coordinate.

c. You must produce the same smallest and largest element as bigsmall.c.

d. Leave the code that measures the time taken to do the search (circled) in its current place as shown:

Answer the following questions:

Question 3.1 (1 mark)

Explain why the original bigsmall-par.c code produced the wrong results.

Question 3.2 (1 mark)

Question 3.3 (1 mark)
