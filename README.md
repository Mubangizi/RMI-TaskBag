# RMITaskBag

The taskbag runs first.

Then the workers run, and keep polling the taskbag for a pair with the id "Task", through a while loop.

The master adds a single Pair("Task", <ranges\>) to the TaskBag
eg `Pair("Task", "[[1-50],[51-100],[101-150],[151-200],[201-250],[251-300]]")`, this is the task added for finding prime numbers between 1 and 300(inclusive), when the "Task" pair is placed in the taskbag, the master enters a while loop, continuously checking for result pairs

A single worker then removes the "Task" pair (note, it is legit removed by a single worker, so other workers can't access it, so they keep polling)
the worker that gets the "Task" pair removes the first range eg [1-50] and puts back the "Task" pair after removing the range, and it then begins to calculate the primes in the range. (another worker will do the same thing for the "Task" pair that has just been returned by this first worker, until there are no more ranges left, at which point the worker stops checking for "Task" and prints "Work done!")

Everytime a worker is done calculating the primes for a given range, it places the results in the TaskBag, with an id made from the range. if the range is [1-50], the id of the result pair is "1-50" and the value is a list of prime number between 1 and 50(inclusive). remember, the master is polling for results and these are the id's it uses to check for results.

Once the master collects results of all the ranges, it prints them and closes.

Additionally, the master shows progress of how many results it has got so far.
The workers show exactly which ranges they are working on
the taskbag shows which of its (placePair, takePair, removePair) methods has been called and with which keys.

Lastly, to ensure that only one worker can get access to the "Task" at a time, all the methods of the TaskBag are marked with the "synchronized" keyword, which ensures that only one of the three methods is accessed at a time

# How to run the application

## ONE - compile

### linux

`javac -cp .:./jackson-core-2.13.0.jar:./jackson-annotations-2.13.0.jar:./jackson-databind-2.13.0.jar *.java`

### windows

`javac -cp .;.\jackson-core-2.13.0.jar;.\jackson-annotations-2.13.0.jar;.\jackson-databind-2.13.0.jar *.java`

## TWO - start registry

### linux

**(leave the terminal open after this command, use a different terminal for the commands below)**
`rmiregistry &`

## windows

**(a new terminal window opens if successful, leave this window open)**

`start rmiregistry`

--------------------------------------------------------------------------
**NOTE: RUN THE COMMANDS BELOW IN SEPARATE TERMINALS**

**NOTE: YOU CAN CREATE AS MANY WORKERS AS YOU LIKE (IN SEPARATE TERMINALS)**

--------------------------------------------------------------------------

## THREE - start task bag

### linux

`java -cp .:./jackson-core-2.13.0.jar:./jackson-annotations-2.13.0.jar:./jackson-databind-2.13.0.jar -Djava.rmi.server.codebase:file:./ TaskBag`

### windows

`java -cp .;.\jackson-core-2.13.0.jar;.\jackson-annotations-2.13.0.jar;.\jackson-databind-2.13.0.jar -Djava.rmi.server.codebase:file:.\ TaskBag`

## FOUR - start worker(s)

### linux

`java -cp .:./jackson-core-2.13.0.jar:./jackson-annotations-2.13.0.jar:./jackson-databind-2.13.0.jar Worker <hostname>`

### windows

`java -cp .;.\jackson-core-2.13.0.jar;.\jackson-annotations-2.13.0.jar;.\jackson-databind-2.13.0.jar Worker <hostname>`

## FIVE - start master

### linux

`java -cp .:./jackson-core-2.13.0.jar:./jackson-annotations-2.13.0.jar:./jackson-databind-2.13.0.jar Master <hostname>`

### windows

`java -cp .;.\jackson-core-2.13.0.jar;.\jackson-annotations-2.13.0.jar;.\jackson-databind-2.13.0.jar Master <hostname>`
