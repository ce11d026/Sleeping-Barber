Sleeping Barber Simulation in C
===============

[Sleeping Barber](http://en.wikipedia.org/wiki/Sleeping_barber_problem) simulation with simultaneous processes, random delays, and semaphores implemented via pipes.

## Requirements
* When the barber finishes cutting hair, he checks the waiting room and gets the next customer. If no customers are waiting, he goes to sleep
* Each arriving customer wakes up sleeping Barber
* Each arriving customer checks for empty chairs in the waiting. If no chairs are available, the customer leaves

Rather than running in an infinite loop, this simulation starts 5 customers simultaneously.  Each customer is capable of triggering a 2nd customer to arrive after they're done.  The barber process is set to run a maximum of 10 times to theoretically handle all 10 customers.  The shop only has a total of 3 seats so customers could possibly be turned away.

* Waiting time uses 0-900 million nanoseconds (0.0 - 0.9 seconds).

* Because reading an empty pipe causes a delay, semaphores are implemented using pipes reading and writing nonsense data (int a=1)

* To communicate the value of the number of empty seats between processes, there is another pipe called "freeseats".  This pipe should always have one integer value stored in it representing the number of free seats available. When reading to retrieve the number of free seats, write is immediately used afterwards to place the value of free seats back into the pipe.

* At the end of the Main procedure, the program waits for 10 seconds and then prints "done".  This is done solely for cleaning up the output.

* A completely different seed time is used for each process for randomization.

Sample Run 1
===

```
$ ./barber
Barber 1 is trying to get a customer
New customer trying to find a seat
Customer is decreasing the number of free seats to 2
New customer trying to find a seat
Barber 1 is waiting for the seat to become free
Barber 1 is increasing the number of free seats to 3
New customer trying to find a seat
Barber is now cutting hair 1
  - wait: 661836814
Customer is decreasing the number of free seats to 2
New customer trying to find a seat
Customer is now waiting for the barber
Customer is now waiting for the barber
Customer is now getting a hair cut
Customer is decreasing the number of free seats to 1
  - wait: 336336314
New customer trying to find a seat
Customer is now waiting for the barber
Customer is decreasing the number of free seats to 0
Customer is now waiting for the barber
Customer giving up: No free chairs in waiting room
  - wait: 489735958
New customer trying to find a seat
Customer giving up: No free chairs in waiting room
  - wait: 102353785
New customer trying to find a seat
Customer giving up: No free chairs in waiting room
  - wait: 788800617
Barber 2 is trying to get a customer
Barber 2 is waiting for the seat to become free
Barber 2 is increasing the number of free seats to 1
Barber is now cutting hair 2
  - wait: 312533810
Customer is now getting a hair cut
  - wait: 799926745
Barber 3 is trying to get a customer
Barber 3 is waiting for the seat to become free
Barber 3 is increasing the number of free seats to 2
Barber is now cutting hair 3
  - wait: 93120126
Customer is now getting a hair cut
  - wait: 58087587
New customer trying to find a seat
Customer is decreasing the number of free seats to 1
Customer is now waiting for the barber
Barber 4 is trying to get a customer
Barber 4 is waiting for the seat to become free
Barber 4 is increasing the number of free seats to 2
Barber is now cutting hair 4
  - wait: 777375375
Customer is now getting a hair cut
  - wait: 11657576
New customer trying to find a seat
Customer is decreasing the number of free seats to 1
Customer is now waiting for the barber
New customer trying to find a seat
Customer is decreasing the number of free seats to 0
Customer is now waiting for the barber
Barber 5 is trying to get a customer
Barber 5 is waiting for the seat to become free
Barber 5 is increasing the number of free seats to 1
Barber is now cutting hair 5
  - wait: 93223175
Customer is now getting a hair cut
  - wait: 593491966
Barber 6 is trying to get a customer
Barber 6 is waiting for the seat to become free
Barber 6 is increasing the number of free seats to 2
Barber is now cutting hair 6
  - wait: 785860826
Customer is now getting a hair cut
  - wait: 75570814
Barber 7 is trying to get a customer
Barber 7 is waiting for the seat to become free
Barber 7 is increasing the number of free seats to 3
Barber is now cutting hair 7
  - wait: 111285651
Customer is now getting a hair cut
  - wait: 628774546
Barber 8 is trying to get a customer

done
```

Sample Run 2
===
```
$ ./barber
Barber 1 is trying to get a customer
New customer trying to find a seat
Customer is decreasing the number of free seats to 2
New customer trying to find a seat
Barber 1 is waiting for the seat to become free
Barber 1 is increasing the number of free seats to 3
New customer trying to find a seat
Barber is now cutting hair 1
  - wait: 269057189
Customer is now waiting for the barber
Customer is now getting a hair cut
Customer is decreasing the number of free seats to 2
  - wait: 694578860
Customer is now waiting for the barber
New customer trying to find a seat
New customer trying to find a seat
Customer is decreasing the number of free seats to 1
Customer is now waiting for the barber
Customer is decreasing the number of free seats to 0
Customer is now waiting for the barber
Customer giving up: No free chairs in waiting room
  - wait: 551248578
Barber 2 is trying to get a customer
Barber 2 is waiting for the seat to become free
Barber 2 is increasing the number of free seats to 1
Barber is now cutting hair 2
  - wait: 298003031
Customer is now getting a hair cut
  - wait: 80480524
New customer trying to find a seat
Customer is decreasing the number of free seats to 0
Customer is now waiting for the barber
New customer trying to find a seat
Customer giving up: No free chairs in waiting room
  - wait: 95211713
Barber 3 is trying to get a customer
Barber 3 is waiting for the seat to become free
Barber 3 is increasing the number of free seats to 1
Barber is now cutting hair 3
  - wait: 168756520
Customer is now getting a hair cut
  - wait: 407453743
New customer trying to find a seat
Customer is decreasing the number of free seats to 0
Customer is now waiting for the barber
Barber 4 is trying to get a customer
Barber 4 is waiting for the seat to become free
Barber 4 is increasing the number of free seats to 1
Barber is now cutting hair 4
  - wait: 291823750
Customer is now getting a hair cut
  - wait: 110152926
New customer trying to find a seat
Customer is decreasing the number of free seats to 0
Customer is now waiting for the barber
New customer trying to find a seat
Customer giving up: No free chairs in waiting room
  - wait: 420368387
Barber 5 is trying to get a customer
Barber 5 is waiting for the seat to become free
Barber 5 is increasing the number of free seats to 1
Barber is now cutting hair 5
  - wait: 210403376
Customer is now getting a hair cut
  - wait: 638861300
Barber 6 is trying to get a customer
Barber 6 is waiting for the seat to become free
Barber 6 is increasing the number of free seats to 2
Barber is now cutting hair 6
  - wait: 212128008
Customer is now getting a hair cut
  - wait: 845465870
Barber 7 is trying to get a customer
Barber 7 is waiting for the seat to become free
Barber 7 is increasing the number of free seats to 3
Barber is now cutting hair 7
  - wait: 743605988
Customer is now getting a hair cut
  - wait: 792143982
Barber 8 is trying to get a customer

done
```

Sample Run 3
===
```
$ ./barber
Barber 1 is trying to get a customer
New customer trying to find a seat
New customer trying to find a seat
New customer trying to find a seat
Customer is decreasing the number of free seats to 2
Customer is now waiting for the barber
Barber 1 is waiting for the seat to become free
New customer trying to find a seat
Barber 1 is increasing the number of free seats to 3
Barber is now cutting hair 1
  - wait: 27559666
New customer trying to find a seat
Customer is decreasing the number of free seats to 2
Customer is now getting a hair cut
Customer is now waiting for the barber
  - wait: 811011
Customer is decreasing the number of free seats to 1
Customer is now waiting for the barber
Customer is decreasing the number of free seats to 0
Customer is now waiting for the barber
Customer giving up: No free chairs in waiting room
  - wait: 293270465
New customer trying to find a seat
Customer giving up: No free chairs in waiting room
  - wait: 818780326
Barber 2 is trying to get a customer
Barber 2 is waiting for the seat to become free
Barber 2 is increasing the number of free seats to 1
Barber is now cutting hair 2
  - wait: 319510843
Customer is now getting a hair cut
  - wait: 167745747
New customer trying to find a seat
Customer is decreasing the number of free seats to 0
Customer is now waiting for the barber
New customer trying to find a seat
Customer giving up: No free chairs in waiting room
  - wait: 446963084
Barber 3 is trying to get a customer
Barber 3 is waiting for the seat to become free
Barber 3 is increasing the number of free seats to 1
Barber is now cutting hair 3
  - wait: 515320765
Customer is now getting a hair cut
  - wait: 35127426
New customer trying to find a seat
Customer is decreasing the number of free seats to 0
Customer is now waiting for the barber
Barber 4 is trying to get a customer
Barber 4 is waiting for the seat to become free
Barber 4 is increasing the number of free seats to 1
Barber is now cutting hair 4
  - wait: 390942228
Customer is now getting a hair cut
  - wait: 613472227
Barber 5 is trying to get a customer
Barber 5 is waiting for the seat to become free
Barber 5 is increasing the number of free seats to 2
Barber is now cutting hair 5
  - wait: 323261380
Customer is now getting a hair cut
  - wait: 252504233
New customer trying to find a seat
Customer is decreasing the number of free seats to 1
Customer is now waiting for the barber
Barber 6 is trying to get a customer
Barber 6 is waiting for the seat to become free
Barber 6 is increasing the number of free seats to 2
Barber is now cutting hair 6
  - wait: 815493759
Customer is now getting a hair cut
  - wait: 793320310
Barber 7 is trying to get a customer
Barber 7 is waiting for the seat to become free
Barber 7 is increasing the number of free seats to 3
Barber is now cutting hair 7
  - wait: 455890733
Customer is now getting a hair cut
  - wait: 126108282
Barber 8 is trying to get a customer

done
```
