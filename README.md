# DevOps Cheat Sheet
## Linux
### Bash


**Redirections:**
Using **>** sign redirects text or output of program to resource such as file or bin, if file not exists it will create as well

    echo “This is file.txt” > file.txt
    echo "This will go to nowhere" > /dev/null
Using **>>** causes appending new line to already existing file, as before it automatically can create file

    echo "This is another line in my file" > file.txt
  Taking arguments into the program or command can be redirect by **<**, called stdin, takes arguments and provides as a content

    cat < file.txt

### SSH
Connecting to server goes by using **ssh** program and for maintaing ssh server **sshd** service is used

    #Connect to server.com with specified user as logged in
    ssh user@server.com
    
    #If server doesnt use default port then port can be customized
    ssh -p 2222 user@server.com

	#Sometimes private key is needed to authorize, in this case providing one is needed
	ssh -i /var/ssh_keys/key.pub user@server.com

There is special subcommand of ssh - **scp** uses ssh mechanism for transfering files between units

    #Sends file.txt to home directory of user
    scp file.txt user@server.com:/home/user/doc/
    
    #Downloading resources can also be used, but it requires replacing the order of both inputs
    scp user@server.com:/home/user/doc/file.txt ./file.txt

Another command related to ssh communication is **rsync**, efficient utility for synchronizing files between local and remote server

    #Process will make sure that remote_dir and local_dir will have the same content
    rsync -avz local_dir/ user@server.com:/home/user/remote_dir/

### Text matching and manipulation
**Grep** is the most known program for pattern searching in text, especially romantically combined with prior pipeline **|** apply

    #List all lines where particular text contains in
    grep "localhost" hosts.ini
    cat hosts.ini | grep "localhost"
    
    #Flag -i for case-insensitive
    grep -i "Localhost" hosts.ini
	
	#Flag -c for counting the number of occurances
	cat hosts | grep -c "localhost"

	#Shows 2 lines after and 1 before each line containing the pattern
	grep -A 1 -B 2 "alpine" Dockerfile

When it comes to text manipulation **sed** provides major technical tools for it like parsing and transforming text

    #Replaces all foo occurances with bar
    sed 's/foo/bar/g' file
    
    #Removes all blanks spaces from file
    sed '/^$/d' file.txt
	
	#Takes only apple containig lines and replaces them with orange
	cat fruits_list.txt | grep "apple" | sed 's/apple/orange/g'

### Directories
For creating directories **mkdir** is the only logical choice. 

    #Creates directory locally
    mkdir my_dir
	
	#Creates directory with a former directory tree
	mkdir -p /var/dir1/dir2/dir3

	
