touch - It is used to create empty file 
eg: touch abc.txt 

cat - It is used to read full file without entering the file meaning it will show contents of file
eg: cat abc.txt

head and tail - It is read parts of a file with head you can read the top lines and with tail it will show lines from bottom
eg: head -n 3 abc.txt (It will show top 3 lines of abc.txt if we dont mention number it will print 10 lines by default)
    tail -n 3 abc.txt (It will show bottom 3 lines)

tee (write and display at the same time)
eg: tee "Line 3" abc.txt



karishma@karishma-Vostro-3400:~/Devops/90daysofDevops$ touch notes.txt
karishma@karishma-Vostro-3400:~/Devops/90daysofDevops$ echo "This is my first line" > notes.txt 
karishma@karishma-Vostro-3400:~/Devops/90daysofDevops$ echo "This is my second line I am adding it to notes text file" >> notes.txt 
karishma@karishma-Vostro-3400:~/Devops/90daysofDevops$ echo "Line 3" | tee -a notes.txt
Line 3
karishma@karishma-Vostro-3400:~/Devops/90daysofDevops$ cat notes.txt 
This is my first line
This is my second line I am adding it to notes text file
Line 3
karishma@karishma-Vostro-3400:~/Devops/90daysofDevops$ head -n 2 notes.txt
This is my first line
This is my second line I am adding it to notes text file
karishma@karishma-Vostro-3400:~/Devops/90daysofDevops$ tail -n 2 notes.txt 
This is my second line I am adding it to notes text file
Line 3
karishma@karishma-Vostro-3400:~/Devops/90daysofDevops$ 

