# crontab
Main Menu
The main menu is the main interface for this program and it allows the user to easily execute crontab commands. It lists all the commands that can be executed by the user. These commands are:


The main method uses a while do loop. This loops infinitely while the variable ‘$run’ is equal to true. In the while loop, there is a base case statement which allocates every command (seen above) to a unique case. I decided to go with this method as I felt it made the structure of the program look very readable. You can see very clearly where each command in the menu is executed in the code. The while loop terminates when the command ‘9’ is entered by the user. This happens because in case 9, there is a line which sets the variable ‘$run’ to false which allows the while loop to break, thus terminating the application. If the users enter a string or number that does not equal a command then the base case will output an appropriate error message, asking the user to enter a valid command.

To stylise the title (“Crontab”) in our program I used an online ASCII text signature generator. This website allows you to enter a word and returns a stylised version of that word, using the font style you have picked. In this case, I used the font ‘big’. I felt it made my application look more professional and presentable to the user. 

Display Running Crontabs
To display running crontabs the user must enter ‘1’. The display crontab running crontabs command lists all the jobs in the crontab. To display all the running crontabs I created a method called display. This method takes the file ‘jobs.txt’ (where all the running crontabs are stored) and writes every line to file with an index number appended in front of it. For example:

This lists the details of the job: minute, hour, day, month, day of the week and the command to be executed.

The other option to display the running crontabs would be to use the built-in command:
crontab -l

This command has a similar output but the issue is I wanted to append an index to every running crontab and this command wouldn’t allow me and this was why I didn’t use this method. As I used my own code to create the command I had to add my own validation as well. The validation would output a message to the user if the file neither existed or contained any jobs:
no crontab for ‘username’

Remove/Edit
These methods in the program share a validation check. They only execute if the crontab file ‘jobs.txt’ exists and contains any jobs. If it does not then the user is prompted with a message explaining this.

Insert a Job
To insert a job, the user must press ‘2’. The insert a job command adds a new job to the crontab. It calls the method ins(), which asks the user to enter a minute, hour, day, month and the day of the week. This will be the time the job will be executed. It then asks the user to enter the task. This can be any kind of command or executable file. It stores all these inputs into a variable called ‘$job’. The variable ‘$job’ is then appended to a file called ‘jobs.txt’ which will store the created job. The file ‘jobs.txt’ is then added to the user’s crontab and stored there until it is deleted.

The command for adding the file ‘jobs..txt’ to the crontab is:
crontab jobs.txt

There is rigorous validation on every field that is entered by the user in order to create the job. Every input apart from the command field is encapsulated by a while loop and two conditions. The while loop loops around the field until the user enters a valid value. The first condition checks that the user has entered a number and the second condition checks that the user has entered a number that is within the correct range for that field. There are appropriate error messages if the user enters an invalid value.


Edit a Job
To edit a job, the user must press ‘3’. This edit a job command will show the user the current running crontabs and ask the user which one they would like to be edited. They can choose which one by entering a number which is indexed to that command (Each index refers to the line number that command lies on in the file ‘jobs.txt’). Each number will cohere to a running crontab. For example:

1) 2 1 4 5 1 ls
2) 6 8 4 2 3 cd   	     
3) 15 9 8 2 5 touch

Once the user picks which crontab they want to edit, that selected running crontab will be deleted. It is deleted by using the same method for the remove a job command, called remove. The insert method (used in the ‘insert a job command’) will then be called and the user will be asked to enter in all the jobs details again. Once entered, the job will be added to the file ‘jobs.txt’. This gives the illusion that the user has edited the function.

Remove a Job
The remove command asks the user which job they want to remove. They chose a job by selecting a jobs index. The index refers to the line number of the job in the file. This line number is then passed to the sed command which will take the line out of the file jobs.txt. It does this by outputting the result of the file with the removed job to a temporary file called ‘file.tmp’. The contents of ‘file.tmp’ is then moved to the original file ‘jobs.txt’. The file is then added to crontab again:

sed "${line}d" jobs.txt > file.tmp && mv file.tmp jobs.txt
crontab jobs.txt

Remove All Jobs
The removes all jobs command removes the crontab entirely and all the jobs in the crontab. The command used is:

> jobs.txt

This basically clears the file and once it has been cleared it is added to crontab again.

Exit
The exit command simply prompts the user with a message and then exits the program and returns the user to their current directory in the terminal. 
