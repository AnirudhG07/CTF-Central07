# Symbols and uses
Various Commands can be understood with only use case of symbols (or hiding from fildering using symbols).

## Meaning of symbols
* `/` - for directory seperation
* `?` 
    -  In the context of file globbing, ? matches any single character. For example, ?.txt matches a.txt but not ab.txt. 
    - In the context of parameter expansion, ${varname:?} will cause the shell to throw an error if varname is unset or empty.
* `*` 
    - In the context of file globbing, * matches any number of any characters. For example, *.txt matches a.txt and ab.txt.
    -  In the context of parameter expansion, `$*` expands to the positional parameters, starting from one.
* `#`
    - In the context of a script, # is used to denote a comment. Anything after # on a line is ignored by the shell.
    -  In the context of parameter expansion, `${varname#pattern}` removes the shortest match of pattern from the start of varname.
* `!` - This is used for history expansion in interactive shells. For example, `!$` expands to the last argument of the previous command. It's also used in parameter expansion to reference the names of variables, as in `${!prefix*}`.
* `&` - When used at the end of a command, & causes the command to run in the background. In the context of parameter expansion, `${varname&pattern}` replaces the smallest match of pattern in varname with pattern.
* `|` - This is the pipe operator, used to send the output of one command as the input to another command.
* `> and <` - These are redirection operators. > redirects output to a file, overwriting the file. < reads input from a file. >> appends output to a file.
* `&& and ||` - These are logical operators. && executes the second command only if the first command succeeds. || executes the second command only if the first command fails.
* `" and '` - Double quotes allow variable and command substitution inside them, single quotes do not.

## Wildcards 
Refer <a href="https://tldp.org/LDP/GNU-Linux-Tools-Summary/html/x11655.htm"> Wildcards </a> page for more info.
- `*`  match 0 or more characters, ex. /lib* -> /lib /lib32 /lib64
- `.*`
- `/*/*`
- `./*`
- `[!]` matches any character that is not in the specified range or set, ex. file[!12].txt -> any files from file0.txt-file9.txt, except file1.txt and file2.txt

## Globbing
Refer <a href="https://tldp.org/LDP/abs/html/globbingref.html"> Globbing </a> for more info.

## Uses of _ and [ ] 
* `_ (Underscore)`
    - In shell scripting, `_` is just another character that can be part of a variable name. It's often used in variable names to make them more readable, like file_name or user_id.
    - \** In the context of command line, `_` is a special shell variable in bash that holds the last argument of the previous command executed.

    For example-
    ```bash
    echo hello world
    echo $_  # Outputs 'world'
    ```
* `[] (Square Brackets)`
    - Square brackets are used in several contexts in shell scripting:

    - Square brackets are used to evaluate conditional expressions. For example, [ $a -lt $b ] checks if variable a is less than variable b.
    
    For example- 
    ```bash
    if [ $a -lt $b ]; then
        echo "$a is less than $b"
    fi
    ```

    - Square brackets are used for array indexing.
    ```bash
    arr=(1 2 3 4 5)
    echo ${arr[2]}  # Outputs '3'
    ```
    -  In file globbing and regular expressions, square brackets define a character class. For example, [abc] matches any one of 'a', 'b', or 'c'.
    ```bash
    ls *[abc]*  # Lists files whose names contain either 'a', 'b', or 'c'

    ls *[1-9]*  # Lists files whose names contain any digit from 1 to 9
    ```

## Use of / and ?
This is a very weird use case. This is not a fixed usecase but is a bit different for each problem's machine.

First thing you can try is -
- `?`  match 1 character, ex. /??? -> /bin /dev /etc /lib
- Try using `/?`, `/??`, `/???`, etc. and see which gives what. These are for obtaining 1,2,3 length directory names.
- Then try `/????/???` and some combinations for traversing within `/????` directory.
- If you do `/????64`, it says you are looking for a file/directory which has 4 characters in the name ending with 64, like `/base64`, etc.
- You can try wildcards pattern like `/???[!_]64`, to ignore 4th character as `_`. 

## Use of \$(), ${}

* `$() (Command Substitution)` This is used for command substitution. The shell will execute the command inside the parentheses, and replace the entire $() expression with the output of the command. This is useful when you want to use the output of a command as an argument to another command.
    ```bash
    echo "Today's date is $(date)"  # Outputs "Today's date is ", followed by the current date and time
    ```
    You can also use backticks (``) for command substitution, but $() is preferred because it is easier to read and can be nested.

* `${} (Parameter Expansion)` This is used for parameter expansion. It allows you to manipulate the value of a variable in various ways. Here are some examples:

    - Variable Substitution: `${varname}` is equivalent to `$varname`. It's useful when you want to append something directly to the value of a variable, because `${varname}suffix` is clearer than `$varnamesuffix`.
    ```bash
    filename="file"
    echo "${filename}.txt"  # Outputs 'file.txt'
    ```

    - Default Values: `${varname:-default}` will use default if varname is unset or empty.
    ```bash
    echo "${uninitialized:-default}"  # Outputs 'default'
    ```

    - Error on Unset: `${varname:?}` will cause the shell to throw an error if varname is unset or empty.
    ```bash
    echo "${uninitialized:?}"  # Throws an error
    ```

    - Substring Removal: `${varname#pattern}` removes the shortest match of pattern from the start of varname. ${varname##pattern} removes the longest match.
    ```bash
    filename="file.txt"
    echo "${filename#*.}"  # Outputs 'txt'
    echo "${filename##*.}"  # Also outputs 'txt'
    ```

    - Substring Replacement: `${varname/pattern/replacement} `replaces the first match of pattern in varname with replacement. ${varname//pattern/replacement} replaces all matches.
    ```bash
    filename="file.txt"
    echo "${filename/t/T}"  # Outputs 'File.txt'
    echo "${filename//t/T}"  # Outputs 'File.TxT'
    ```