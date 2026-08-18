Task 1: Your First Script

Create a file hello.sh
Add the shebang line #!/bin/bash at the top
Print Hello, DevOps! using echo
Make it executable and run it

karishma@MyPc:~/practice$ vi hello.sh
karishma@MyPc:~/practice$ chmod +x hello.sh 
karishma@MyPc:~/practice$ ./hello.sh 
Hello, DevOps!
karishma@MyPc:~/practice$ 


*******************************************************************

Task 2: Variables

    Create variables.sh with:
        A variable for your NAME
        A variable for your ROLE (e.g., "DevOps Engineer")
        Print: Hello, I am <NAME> and I am a <ROLE>
    Try using single quotes vs double quotes — what's the difference?
    
karishma@MyPc:~/practice$ vi variables.sh
karishma@MyPc:~/practice$ chmod +x variables.sh 
karishma@MyPc:~/practice$ ./variables.sh 
Hello, I am Karishma and I am a DevOps Engineer
karishma@MyPc:~/practice$ 


karishma@MyPc:~/practice$ cat variables.sh 
#!/bin/bash

NAME="Karishma"
ROLE="DevOps Engineer"

echo "Hello, I am $NAME and I am a $ROLE"

# single and double quotes

NAME="Alice"
echo "Hello, $NAME"

NAME="Alice"
echo 'Hello, $NAME'
karishma@MyPc:~/practice$ ./variables.sh 
Hello, I am Karishma and I am a DevOps Engineer
Hello, Alice
Hello, $NAME
karishma@MyPc:~/practice$ 

**************************************************************
Task 3: User Input with read

    Create greet.sh that:
        Asks the user for their name using read
        Asks for their favourite tool
        Prints: Hello <name>, your favourite tool is <tool>


arishma@MyPc:~/practice$ cat greet.sh 
#!/bin/bash

read -p "Enter your name: " name
read -p "Enter your favourite tool: " tool

echo "Hello $name, your favourite tool is $tool"
karishma@MyPc:~/practice$ ./greet.sh 
Enter your name: karu
Enter your favourite tool: jenkins
Hello karu, your favourite tool is jenkins
karishma@MyPc:~/practice$ 


**********************************************************************
Task 4: If-Else Conditions

  A]  Create check_number.sh that:
        Takes a number using read
        Prints whether it is positive, negative, or zero

    
at check_number.sh 
#!/bin/bash

read -p "Enter a number: " number

if [ "$number" -gt 0 ]; then
    echo "The number is positive"
elif [ "$number" -lt 0 ]; then
    echo "The number is negative"
else
    echo "The number is zero"
fi
karishma@MyPc:~/practice$ chmod +x check_number.sh 
karishma@MyPc:~/practice$ ./check_number.sh 
Enter a number: 4
The number is positive
karishma@MyPc:~/practice$ ./check_number.sh 
Enter a number: 9
The number is positive
karishma@MyPc:~/practice$ ./check_number.sh 
Enter a number: -6
The number is negative
karishma@MyPc:~/practice$ 

B ] Create file_check.sh that:
        Asks for a filename
        Checks if the file exists using -f
        Prints appropriate message

cat check.sh 
#!/bin/bash

read -p "Enter a filename: " filename

if [ -f "$filename" ]; then
    echo "The file exists"
else
    echo "The file does not exist"
fi
karishma@MyPc:~/practice$ chmod +x check.sh 
karishma@MyPc:~/practice$ ./check.sh 
Enter a filename: abc
The file does not exist
karishma@MyPc:~/practice$ ./check.sh 
Enter a filename: check
The file does not exist
karishma@MyPc:~/practice$ ./check.sh 
Enter a filename: check.sh
The file exists
karishma@MyPc:~/practice$ 


************************************************************************

Task 5: Combine It All

Create server_check.sh that:

    Stores a service name in a variable (e.g., nginx, sshd)
    Asks the user: "Do you want to check the status? (y/n)"
    If y — runs systemctl status <service> and prints whether it's active or not
    If n — prints "Skipped."


vi server_check.sh
karishma@MyPc:~/practice$ chmod +x server_check.sh 
karishma@MyPc:~/practice$ ./server_check.sh 
Do you want to check the status? (y/n) y
nginx is not active.
Unit nginx.service could not be found.
karishma@MyPc:~/practice$ vi server_check.sh
karishma@MyPc:~/practice$ ./server_check.sh 
Do you want to check the status? (y/n) y
sshd is not active.

********************************************************************



