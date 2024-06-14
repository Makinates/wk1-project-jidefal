# Wk1 Task 1 - Network Fundamentals 

- I am working on a project to Configure virtual machines or cloud instances with different network configurations (e.g., subnets, VPCs, security groups, and network access control lists).
- Set up and test network connectivity between instances using ping, telnet and other tools.
- Analyze network traffic using packet-capturing tools like wireshark and tcpdump 

I will follow these example scenario 
1. Create a VPC with CIDR block 10.0.0.0/16
2. Create two subnets: One public subnets (10.0.0.0/17) and private (10.0.128.0/17)
3. Create an internet gateway and attach it to the VPC. 
4. Create security groups and NACL to allow/deny traffic. 
5. Launch instances in both subnets and configure them to use the appropriate security group and NACLS. 
6. Use tools like `ping` and `telnet` to test the connectivity.

This setup provides a basic configuration for VPC with different network configuration like subnets, security groups, and NACLs. 


# Task 2 - Monitoring and Logging 
- Install and configure a monitoring solution like Prometheus
- Create custom metrics and alerts for monitoring system resources (CPU, memory, disk, etc.)
- Set up log aggregation and analysis using tools like ELK Stack (Elasticsearch, Logstash, and Kibana)
- Write queries to analyze and visualize log data for troubleshooting and performance optimization

# Task 3 - Linux Fundamentals

- Familiarize with the Linux file system hierarchy and navigate the file system using command-line tools (e.g., cd, ls, pwd, mkdir, rm)
- Manage files and directories using commands like cp, mv, touch, chmod, and chown
- Use text editors like vim or nano to create, edit, and manipulate text files
- Leverage command-line tools for system administration tasks (e.g., ps, top, df, du, lsof, netstat).


# Task 4 - Command-Line Scripting 

- Write and excute basic Bash scripts to automate repetitive tasks.
- Implement control structures (e.g., if-else, loops) and variables in Bash scripts.
- Utilize command-line text processing utilities like grep, sed, awk, and cut.
- Automate system administration tasks using Bash scripts (e.g., user management, log rotation, backups)

## Pre-requisite 
- AWS free tier account 
- Github account 
- [visual subnet calculator](https://www.davidc.net/sites/default/subnets/subnets.html)
- Linux terminal
- [Chmod Wiki](https://en.wikipedia.org/wiki/Chmod)
- ChatGPT

