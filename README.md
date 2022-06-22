# RMITaskBag

ONE - compile
#linux
javac -cp .:./jackson-core-2.13.0.jar:./jackson-annotations-2.13.0.jar:./jackson-databind-2.13.0.jar *.java

#windows
javac -cp .;.\jackson-core-2.13.0.jar;.\jackson-annotations-2.13.0.jar;.\jackson-databind-2.13.0.jar *.java

TWO - start registry
#linux (leave the terminal open after this command, use a different terminal for the commands below)
rmiregistry &

#windows (a new terminal window opens if successful, leave this window open)
start rmiregistry

--------------------------------------------------------------------------
NOTE: RUN THE COMMANDS BELOW IN SEPARATE TERMINALS

NOTE: YOU CAN CREATE AS MANY WORKERS AS YOU LIKE (IN SEPARATE TERMINALS)


THREE - start task bag
#linux
java -cp .:./jackson-core-2.13.0.jar:./jackson-annotations-2.13.0.jar:./jackson-databind-2.13.0.jar -Djava.rmi.server.codebase:file:./ TaskBag

#windows
java -cp .;.\jackson-core-2.13.0.jar;.\jackson-annotations-2.13.0.jar;.\jackson-databind-2.13.0.jar -Djava.rmi.server.codebase:file:.\ TaskBag

FOUR - start worker(s)
#linux
java -cp .:./jackson-core-2.13.0.jar:./jackson-annotations-2.13.0.jar:./jackson-databind-2.13.0.jar Worker <hostname>

#windows
java -cp .;.\jackson-core-2.13.0.jar;.\jackson-annotations-2.13.0.jar;.\jackson-databind-2.13.0.jar Worker <hostname>


FIVE - start master
#linux
java -cp .:./jackson-core-2.13.0.jar:./jackson-annotations-2.13.0.jar:./jackson-databind-2.13.0.jar Master <hostname>

#windows
java -cp .;.\jackson-core-2.13.0.jar;.\jackson-annotations-2.13.0.jar;.\jackson-databind-2.13.0.jar Master <hostname>