# Useful Bash commands

## sed
### Change files content 
```bash
sed -i 's/search_string/replace_string/' filenames
```

**‘-i’** option is used to modify the content of the original file with the replacement string if the search string exists in the file.

**Make a backup copy with** `-i.bak` and will create a copy with .bak extension

**‘s’** indicates the substitute command.

## SSH
### Connect to remote host to stablish proxy in your machine
`ssh -L <port_in_your_machine>:<remote_private_internal_ip>:<remote_port> -i /path/to/private_key user@<remote_public_ip> -N`

Example remote connection to MySQL

`ssh -L 33061:remote_internal_ip:3306 -i ~/keys/key elvato@ip -N`
