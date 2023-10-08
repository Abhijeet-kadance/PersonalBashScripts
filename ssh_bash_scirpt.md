# Bash Script to SSH to Server Using an Integer Argument

This Bash script allows you to SSH to a server by providing an integer argument, which corresponds to a server number defined in a text file. Each server in the text file is associated with a unique number.

## Usage

1. Create a text file named `server_list.txt` with the following format:

   ```
   1 server1.example.com
   2 server2.example.com
   3 server3.example.com
   ```

   Replace `server1.example.com`, `server2.example.com`, etc., with the actual server names or IP addresses you want to SSH into. Assign a unique number to each server.

2. Create the Bash script with the following content, and save it as `ssh_to_server.sh`:

   ```bash
   #!/bin/bash

   # Check if the server list file exists
   if [ ! -f "server_list.txt" ]; then
     echo "Server list file 'server_list.txt' not found. Please create the file with server information."
     exit 1
   fi

   # Check if the argument is provided
   if [ "$#" -ne 1 ]; then
     echo "Usage: $0 <server_number>"
     exit 1
   fi

   # Get the server number from the argument
   server_number="$1"

   # Find the corresponding server name in the list
   server_name=$(grep "^$server_number " "server_list.txt" | awk '{print $2}')

   # Check if the server number exists in the list
   if [ -z "$server_name" ]; then
     echo "Server number $server_number not found in the server list."
     exit 1
   fi

   # SSH to the server
   echo "Connecting to $server_name..."
   ssh "$server_name"
   ```

3. Make the script executable:

   ```bash
   chmod +x ssh_to_server.sh
   ```

4. To SSH to a specific server, run the script with the server number as an argument. For example, to SSH to "server2.example.com" (as per the example server list above), run:

   ```bash
   ./ssh_to_server.sh 2
   ```

   This will check the provided integer argument, look up the corresponding server name in the `server_list.txt` file, and then SSH to the specified server.

---

This Markdown guide provides step-by-step instructions for creating and using the Bash script to SSH to servers based on an integer argument and a server mapping text file.


---

<div style="text-align: center;">
👾 Created by Abhijeet Thorat 👾
<br>
Follow me for more on <a href="https://github.com/Abhijeet-kadance"> ✨GitHub✨</a>
</div>