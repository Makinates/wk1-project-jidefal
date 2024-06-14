# Wk1 Task 1 - Network Fundamentals 

## Sub-task 1 

We will build a setup that provides a basic configuration for a VPC with different network configurations like subnets, security groups and NACLS. 

### Step 1 - Create a VPC (Virtual Private Cloud)

Go to the AWS management console, search for VPC via the search bar. 
![VPC search](<Images/SC 02 - VPC search.PNG>)

**Click VPC** and then Click Create VPC

Selecet VPC only, give your VPC a name 
![VPC creation](<Images/SC 03 - VPC creation.PNG>)

Click **create VPC**. 

![VPC page](<Images/SC 05 VPC page.PNG>)

### Step 2 - Add subsets to your VPC 

1. Go to VPC, Select Subnets in the left navigation pane of the amazon VPC console and then Click **create Subnet**

2. When you get to the Subnet Page. Select the VPC you just created. Give your new subnet a name and select the availability Zone.

3. Following this [visual subnet calculator](https://www.davidc.net/sites/default/subnets/subnets.html) for CIDR block creation, 
![CIDR creation](<Images/SC 01 - Subnet CIDR.PNG>). we will create the CIDR block for the first public subnet, then input the CIDR block in the IPV4 CIDR block section. 

After filling all the other requirements. Click **create subnet**.

![Subnet creation](<Images/SC 04 - Subnets Creation.PNG>)

4. The same steps will be done carried for the second subnet but the availability zone will be different.  

### Step 3 - Create Route Table 

1. Go to VPC, Select Route tables in the left navigation pane of the amazon VPC console. Then **click create route table**. 

2. Give the route table a name, Select the VPC you have create then click **create route table**

![Create route table](<Images/SC 06 - Route table.PNG>)

3. Associate the subnets explicit to the route 
Click on subnet association, click on **edit subnet association** then add the two subnets you created 

![route table association](<Images/SC 07 - Route table association.PNG>)

### Step 4 - Create an Internet Gateway 

1. GO to VPC, select internet gateway in the left navigation pane of the amazon VPC console . Click **Create internet gateway**.
![IGW](<Images/SC 08 - Internet Gateway.PNG>)

2. Define the route. 
You will attach the internet gateway to the VPC, Click on the button at the top right corner 
![attach VPC](<Images/SC 09 - attach VPC.PNG>)

3. You associate the Internet gateway with the Public subnet.
- Select the route table associated with your public subnet. 
- Select the route table, the Edit routes. 
- Add route: Destination: `0.0.0.0/0`
Target: internet Gateway Id (The internet gateway created).

 ![IGW route table](<Images/SC 10 - IGW attached to the route table.PNG>)

 ### Step 5 - Configure the Network ACLs

 Network ACLs are stateless and can be used to control traffic at the subnet level. Each subnet in a VPC must bbe associated with a network ACL. 

 Follow the steps to configure:
 1. In the left navigation pane of the amazon VPC console, click on **Network ACLs** under **Security**.
 2. Click on **Create network ACL**
 3. COnfigure the network ACl:
 - **Name tag**: Provide a name for your network ACL
 - **VPC**: Select the VPC where your subnets are located. 
 4. After creating the network ACL, configure its inbound and outbound rules
 5. After configuring the ACL, Associate it with your subnets:
 - Select the network ACL, click on **Actions** and choose **Edit subnet associations**.
 - Add the subnets where you want to apply the network ACL. 

![NACL creation](<Images/SC 11 - NACL.PNG>)


## Subtask 2 

I am setting up and testing network connectivity between instances using ping, telnet.
Setting up and testing network connectivity between instances involves ensuring that your network configuration created (VPC, subnets, security groups and Network ACLs) are correctly set up, and then using tools like `ping` and `telnet` to test the connectivity.

### Step 1: Ensure the instances are launched are configured

1. Launch an EC2 instance
- we will launch two instances in the VPC created. They will be in different subnets as we are testing cross-subnet communication. 

Instance 1 Creation 

![Creating Instance 1](<Images/SC 13 - Creating First Instance.PNG>)

Instance 2 Creation

![Creating Instance 2](<Images/SC 14 - Creating Second Instance.PNG>)

The two instances are Launched and they are running succesfully. Each instance is deployed in different availability zone. 

![Sucessfully Launched Instances](<Images/SC 15 - Two instances successfully Launched.PNG>)

2. Configure Security Groups
- Ensure the security groups attached to the instances allow the necessary inbound and outbound traffic.
- For `ping` (ICMP), allow ICMP traffic. 
- For `telnet` (TCP), allow inbound traffic on the specific port ypu will test (port 23 for telnet).

![Creating Security Group](<Images/SC 12 - Creating Security Group.PNG>)

### Step 2: Test Connectivity Using Ping 

1. Connect to your Instances: 

- Use SSH to connect to your instances. 
To do that, select the instance and **connect** button at the top right corner of your window. Then click on the **SSH Client** tab 

![SSH connect](<Images/SC 16 - SSH coneect.PNG>)

- Go to your computer's terminal, cd to the location you saved the key pairs you created while launching your instance. 

<Image>
2. Ping between Instances
- Obtain the IP address of the target instance 
<Images>
- On the source instance run `ping` command
<Images>

### Step 3: Test Connectivity Using Telnet 

1. Install Telnet 

On AmazonLinux using the command 

```bash 
sudo yum install telnet -y
```
<Image>

2. Telnet to Target Instance
- Run the `Telnet` command from the source instance to the target instance's IP and port 

<Image>


# Wk1 Task 3 - Linux Fundamentals

## Subtask 1 

Familiarize with the Linux file system hierarchy and navigate the file system using command-line tools (e.g., cd, ls, pwd, mkdir, rm)

The linux file system hierarchy follows a standard structure known as the Filesystem Hierarchy standard (FHS). This structure is designed to provide a consistent layout and organisation of files and directories. 

### `pwd` (Print working Directory) 
Displays the current directory you are in. 

```bash
pwd
```

### `ls` (List) 
Lists the contents of a directory. 

```bash 
ls          # List files in the current directory
ls -l       # List files with detailed information
ls -a       # List all files, including hidden files
ls -lh      # List files with human-readable file sizes
```

### `cd` (Change Directory) 
Changes the current directory. 

```bash 
cd /path/to/directory   # Change to a specific directory
cd ~                    # Change to the home directory
cd ..                   # Go up one directory level
cd -                    # Go to the previous directory
```

### `mkdir` (Make Directory)
Creates a new directory. 

```bash 
mkdir new_directory   # Create a single new directory
mkdir -p dir1/dir2    # Create nested directories
```

### `rmdir` (Remove Directory)
Remove an empty directory. 

```bash 
rmdir directory_name   # Remove an empty directory
```

### `rm` (Remove)
Removes files or Directories 

```bash 
rm file_name                  # Remove a file
rm -r directory_name          # Remove a directory and its contents recursively
rm -f file_name               # Force remove a file
rm -rf directory_name         # Force remove a directory and its contents recursively
```

We will do a practical task of creating a new directory, navigating through it, and then cleaning it up. we will follow these Steps:
1. Create a directory called 'makinate-prjt'
2. Inside the directory, create a subdirectory called 'pepper'
3. Change directory to the pepper directory and create a file callled "real.txt"
4. List the content of "pepper" to verify the file was created. 
5. Move up to 'makinate-prjt' directory and remove the 'pepper' directory along with its content.

![Linux Ubuntu Home](<Images/SCA 01 - Linux home directory page.PNG>) 

On Ubuntu, i have done with the command given:
- Check my Current Directory with `pwd` 
- List the contents of the Root Directory `ls /`
- Change to Home Directory `cd ~`

1. Create a New Directory 
![Creating a New Directory](<Images/SCA 02 - Make directory.PNG>)

2. Change to the New DIrectory
![Change to the new directory](<Images/SCA 03 - Change directory.PNG>)

3. Create a New File in the Directory 

I created a subdirectory called pepper. Inside a pepper, I created a text file  
![Create a txt file ](<Images/SCA 04 - create txt file.PNG>)

4. List the contents of the Directory: 
![Listing the content of the directory](<Images/SCA 05 - List the content in the Directory.PNG>)

5. Move up to 'makinate-prjt' directory and remove the 'pepper' directory along with its content

I moved up to the parent directory and listed the content in that directory. 
![move up the directory](<Images/SCA 06 - Move up the directory.PNG>)

I used the `rmdir` to remove the directory. I got an error message because the directory wasn't empty. I also tried the `rm` command. It didn't work as shown in the screenshot below. 

I used the `rm -r` command which removes a directory and its content recursively.

![Remove directory](<Images/SCA 07 - Remove Directory.PNG>)

I tend listed the content of the present file and it shows there is no directory present. 


## Subtask 2 
An overview of managing files and directories using commands like `cp`,`mv`, `touch`, `chmod`, and `chown`. 

### `cp`(Copy)
The `cp` command is used to copy files and directories. 

```bash 
cp source_file destination_file   # Copy a file to another file
cp source_file /path/to/directory # Copy a file to a directory
cp -r source_directory destination_directory  # Copy a directory and its contents recursively
```
### `mv` (Move or Rename)
The `mv` command is used to move or rename files and directories. 

```bash 
mv old_file new_file                   # Rename a file
mv file /path/to/directory             # Move a file to another directory
mv -r source_directory destination_directory  # Move a directory and its contents
```

### `touch` (Create or update)
The `touch` command is used to create an empty file or update the timestamp of an existing file. 

```bash
touch file_name                        # Create a new empty file or update the timestamp of an existing file
```

### `chmod` (Change File mode)
The `chmod` command is used to change the permissions of a file or directory. 

```bash 
chmod [options] mode file              # Change the permissions of a file or directory
chmod +x file                          # Add execute permission to a file
chmod -r u+r directory                 # Recursively add read permission to the owner for a directory and its contents
```

Permission are represented by: 
- `r`: Read 
- `w`: Write 
- `x`: Excute 

You can use symbolic (e.g `u`,`g`,`o`,`a`) or numeric (e.g `775`) notation to set permissions: 

- `u`: User 
- `g`: Group 
- `o`: Others 
- `a`: All 

```bash 
chmod 755 script.sh                    # Set read, write, execute for owner; read and execute for group and others
chmod +x script.sh                     # Add execute permission to script.sh
chmod -R u+rwx directory               # Recursively add read, write, and execute permissions to the owner for directory and its contents
```

**Reference:** [Chmod Wiki](https://en.wikipedia.org/wiki/Chmod) 

### `chown` (Change Ownership)
The `chown` command is used to change the owner and group of a file or directory. 

```bash 
chown owner file                       # Change the owner of a file
chown owner:group file                 # Change the owner and group of a file
chown -R owner:group directory         # Recursively change the owner and group of a directory and its contents
```

We will run through a practice task to show the the command:
1. Create a new file called `bigi.txt`. 
2. Copy `bigi.txt` to `bigi_copy.txt`
3. Rename `bigi_copy.txt` to `bigi_backup.txt`
4. Change the permission of `bigi_backup.txt` to read, write, and excute for the owner and read for group and others. 

    1. ![New file](<Images/SCA 08 - Created a new file.PNG>)

    2. ![Copy one file into another](<Images/SCA 09 - Copy one file to another.PNG>)

    3. ![Rename file](<Images/SCA 10 - Rename file.PNG>)

    4. ![Permission Change](<Images/SCA 11 - Change permission of a file.PNG>)


## Subtask 3 

Text editors like `vim` and `nano` are powerful tools for creating, editing and manipulating text files in linux. 

### `nano` Text Editor
`nano` is a user-friendly, easy-to-use text editor ideal for beginners. 
**Basic Commands**

- **Open a file with `nano`:**
```bash 
nano bigi.txt
```
If the file doesn't exist, `nano` will create it. 

![Create a text file](<Images/SCA 12 - nano a text file.PNG>)

- **Editing text:** 
Use the arrow keys to navigate. Type to insert text. 

![edit file](<Images/SCA 13 - Editing a file using Nano.PNG>)

- **Save and Exit:**
    - Save changes: `ctrl + o` then press `Enter` to confirm.
    - Exit `nano`: `ctrl + X`

I used the `cat` command to confirm the edit done on the file 

![cat the file](<Images/SCA 14 - Cating the edited file.PNG>)

### `vim` Text Editor 
`vim` (Vi Improved) is a more advanced text editor with powerful features. 

**Basic Modes**
- Normal mode: The default mode for navigation and commands. 
- Insert mode: For inserting text. Enter by pressing `i` in normal mode.
- Visual mode: For selecting text. Enter by pressing `v` in Normal mode.
- Command mode: For exxcuting commands. Enter by pressing `:` in Normal mode. 

**Basic Commands** 

- Open a file with `vim`: 
```bash
vim bigi_backup.txt
```
If the file doesn't exist, `vim` will create it. 

![Open a file with vim](<Images/SCA 16 - Opening a file with VIM.PNG>)

- Insert text:
    - Press `i` to insert mode. 
    - Type your text. 
    - Press `Esc` to return to normal mode. 

![Editing with vim](<Images/SCA 15 - Editing using VIM.PNG>)

- Save and Exit: 
    - Save changes: `:w` (then press `Enter`).
    - Save and exit: `:wq` or `:x` (then press `Enter`)
    - exit without saving: `:q!` (then press`Enter`)

I used the `cat` command to confirm the edit done on the file

![cat vim file ](<Images/SCA 17 - cat the edited vim file.PNG>)

## Subtask 4 

Leveraging command-line tools for system administration is essential for managing and monitoring a Linux sysytem. Here are some commonly used tools and their basic usage. 

### `ps` (Process Status)

The `ps` command displays information about active processes. 

```bash 
ps                           # Display a snapshot of the current processes
ps aux                       # Show detailed information about all running processes
ps -ef                       # Show detailed information using standard syntax
```
![ps active process](<Images/SCA 19 - ps active process.PNG>)

### `top` (Task Manager)

The `top` command provides a real-time, dynamic view of the running system, including CPU and memory usage. 

```bash 
top                          # Start the top utility
```
**Key Commands within `top`: 
- `q`: Quit `top`
- `h`: Help. 
- `k`: Kill a process (you will be prompted for PID). 
- `r`: Renice a process (Change its priority). 

![top](<Images/SCA 18 - top file maangement.PNG>)

### `df` (Disk Free)

The `df` command reports the amount of disk space used and available on file systems. 

```bash 
df                          # Display disk space usage for all mounted filesystems
df -h                       # Display disk space usage in human-readable format (e.g., KB, MB, GB)
df -T                       # Include the type of filesystem
```
![Disk free](<Images/SCA 20 - Disk free.PNG>)

### `du` (Disk Usage)

The `du` command estimates file space usage. 

```bash 
du                          # Summarize disk usage of each file and directory
du -h                       # Display sizes in human-readable format
du -sh                      # Display total disk usage in human-readable format
du -sh *                    # Display disk usage of each file and directory in the current directory
```
![Disk usage](<Images/SCA 21 - Disk Usage.PNG>)

### `lsof` (List Open Files)

The `lsof` command lists information about files opened by processes. 

```bash 
lsof                        # List all open files
lsof /path/to/file          # List all processes that have the specified file open
lsof -i :port_number        # List all open files associated with the specified port
```
![List Open Files](<Images/SCA 22 - List.PNG>)

### `netstat` (Network Statistics)

The `netstat` command displays network connections, routing tables, interfaces statistics, masquerade connections, multicast memberships. 

```bash 
netstat                     # Display network connections
netstat -a                  # Display all connections and listening ports
netstat -tuln               # Display listening TCP and UDP ports with numeric addresses
netstat -r                  # Display the kernel routing table
```

![network statitics](<Images/SCA 23 - netstat tools.PNG>)

When the **netstat** command was entered. The result returned was command not found. we had to instal **net-tools** before the command could give the required results. 


# WK1 Task 4 - Command-Line Scripting 

Command line scripting involves writing scripts that automate tasks and processes using a command line interface (CLI). These scripts are often written in languages lash bash, Python, Perl, and Powershell 
depending on the operating system and the specific requirements of the tasks. 

some examples of command line scripting: 
 
**1.  Bash Scripting (Linux/MacOS):**
Bash is a common scripting language for unix-based systems. 

```bash 
#!/bin/bash
echo "Hello, World!"
```
**2. Python Scripting:** 
Python scripts can be executed from the command line and are used for complex tasks. 

```python 
#!/usr/bin/env python3
print("Hello, World!")
```
**3. Powershell Scripting:** 
Powershell is a powerful scripting language for windows environments. 

```powershell
Write-Output "Hello, World!"
```

## Substask 1 
Automating repetitive tasks with Bash scripts can greatly enhance efficiency and reduce errors. 

This scripts backs up all `.txt` files from source directory to a backup directory.

### Step 1 - FInd the Working Directory 

Check working directory and create a sample directory to Test your back up.

![working directory check](<Images/SCA 24 - Checking working Directory.PNG>)

### Step 2 - Create a file backup.sh 

To create the file type the command `nano backup.sh`. This command create a backup.dh file and also open the file with nano file editor.

Copy this code below into the editor and save.   

```bash 
#!/bin/bash

# Define the source and backup directories
SOURCE_DIR="/home/jidefal/sample1"
BACKUP_DIR="/home/jidefal"

# Create the backup directory if it doesn't exist
mkdir -p "$BACKUP_DIR"

# Copy all .txt files from source to backup directory
cp "$SOURCE_DIR"/*.txt "$BACKUP_DIR"

# Print a message indicating the backup is complete
echo "Backup complete!"
```

![shell script nano](<Images/SCA 25 - nano shell script.PNG>)

### Step 3 - Execute 

We have to create a sample text file to test run the **backup.sh** script.

![Testing file](<Images/SCA 26 - Testing the file.PNG>)


To execute, make the backup.sh file executable for `chmod +x backup.sh` then type `./backup.sh`

```bash 
chmod +x backup.sh
./backup.sh
```
Here is the result scripts ran

![Results](<Images/SCA 27 - Result of the Script.PNG>)

## Sub-task 2 
Control structures and variables are essential components in Bash scripting, allowing you to create more dynamic and functional scripts. Here is an example demostrating the use of `if-else` statement and variables in Bash scripts. 

Variables in Bash are used to store data that can be referenced later in the script. `if-else` statements allow you to execute different blocks of code based on conditions. 

In the bash script below, the value 5 and 10 are stored in Variable `NUMBER1` and `NUMBER2`. The control structure `if-else` checks if the first variable `NUMBER1` is greater than `NUMBER2`.

```bash 
#!/bin/bash

# Define a variable
NUMBER1=10
NUMBER2=5


# Check if the number is greater than 5
if [ "$NUMBER1" -gt "$NUMBER2" ]; then
    echo "The number is greater than 5."
else
    echo "The number is 5 or less."
fi
```
![nano the variable if-else file](<Images/SCA 28 - Nano var-if-else-sh.PNG>)

The result is shown below. 
![The result](<Images/SCA 29 - var-if-else result.PNG>)

**Challenge:** There was an error in the scripts and shown in the result returned. 

The scripts was editted and the right output was given. 

Below is corrected scripts 

```bash 
#!/bin/bash

# Define a variable
NUMBER1=10
NUMBER2=5


# Check if the number is greater than 5
if [ "$NUMBER1" -gt "$NUMBER2" ]; then
    echo "The $NUMBER1 is greater than $NUMBER2."
else
    echo "The $NUMBER1 is less than $NUMBER2."
fi
```

![Corrected script](<Images/SCA 30 - Corrected script.PNG>)

## Sub-task 3 
Command-line text processing utilities like `grep`, `sed`, `awk` and `cut` are powerful tools for manipulating and analyzing text data in Bash scripts. Here is an example demostrating how to use these utilies 

- `grep` is used to search for patterns within text files. 
- `sed` (stream editor) is used for text substitution and transformation. 
- `awk` is a powerful language for pattern scanning and processing. 
- `cut` is used to extract sections from each line of a file. 

This script below combines these utilities to process a log file, extracts a log file, extracts specific fields, filters lines based on a pattern, and transforms the output. 

```bash 
#!/bin/bash

# Define the log file to process
LOG_FILE="server.log"

# Extract the date, time, and error message from the log file, filter for errors, and format the output
grep "ERROR" "$LOG_FILE" | \
awk '{print $1, $2, $5}' | \
sed 's/\[//g; s/\]//g' | \
cut -d ' ' -f 1-3
```

![nano shell script log file](<Images/SCA 31 - log-sh.PNG>)

Here is result of the execute script 

![Result script](<Images/SCA 32 - log file result.PNG>)

## Sub-task 4
Automating system administration tasks with bash scripts can greatly enhance efficiency and consistency in managing servers. An exmaple script for common administrative task like backup was done in Sub-task 2 above, 