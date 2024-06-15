# Commands tips and tricks
This a list of various Things i can try with some commands which will come in Handy

## echo

### Regular

* `echo $(ls)`
* `echo "CTF" > file.txt`
* `echo "CTF" >> file.txt`
* `echo -e "\x41"`  # Prints 'A' 
`echo -e "\101"`  # Also prints 'A'
* `echo "CTF" | nc localhost 1234` # sending data to server

### Files based

* `echo $(cat file.txt)` # read file and print contents
* `echo $(sed -n '5p' file.txt)`  # Prints the 5th line of file.txt
* `echo $(grep "CTF" file.txt)`  # Prints lines containing "CTF" in file.txt
* `echo $(awk '{print $1}' file.txt)`  # Prints the first field of each line in file.txt
* `ARRAY=($(cat file.txt)); echo ${ARRAY[0]}`  # Prints the first element of the array
* `echo $(<file.txt)`  # for printing file contents

### Encoding Decoding

* `echo -n "CTF" | xxd -p ` # Hex encode
* `echo -n "435446" | xxd -r -p`  # Hex Decode
* `echo "obase=2; $(printf '%d' "'C")" | bc`  # Binary Encode
* `echo "ibase=2; 1000011" | bc | awk '{printf("%c", $1)}'`  # Binary Decode
* `echo "text" | base64 -d `# base64 decode

## Permissions
* `sudo -l` tells which all commands have automatic sudo permissions, this permission error issues can be dealt with those commands.
* `chmod 777 file`, this change permission to `rwxrwxrwx`. But chmod should have permission to change(try with sudo)

## Vi or Vim
* This has a special command you can try- `:! ls -la` or simply `:! <command>`. 
* `:Explore` to explore about file directories within vim.

## grep
* `grep "pattern" file.txt`  # Prints lines containing "pattern" in file.txt
* `grep -i "pattern" file.txt`  # Prints lines containing "pattern", "Pattern", "PATTERN", etc. in file.txt
* `grep -r "pattern" directory/`  # Searches for "pattern" in all files in the directory recursively
* `grep -n "pattern" file.txt ` # Prints lines containing "pattern" in file.txt, along with the line numbers
* `grep -c "pattern" file.txt ` # Prints the number of lines that contain "pattern" in file.txt
* `grep -v "pattern" file.txt`  # Prints lines that do not contain "pattern" in file.txt
* `grep -w "pattern" file.txt`  # Only matches lines where "pattern" is a whole word
* `grep "^pattern" file.txt`  # Matches lines that start with "pattern"
`grep "pattern$" file.txt ` # Matches lines that end with "pattern"
* `grep "pattern" file1.txt file2.txt ` # Searches for "pattern" in both file1.txt and file2.txt
* `grep -o "pattern" file.tx`t  # Prints only the matched parts of a line, not the entire line
