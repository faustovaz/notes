# **Shell**

- [Modes](#modes)
- [Conditionals](#conditionals)
- [Arrays](#arrays)
- [Loops](#loops)
- [Tips](#tips)



### Modes

| mode        | Descritpion                                                  |
| ----------- | ------------------------------------------------------------ |
| -e          | Interrupts the script execution when an error occurrs (when some command returns a non-zero exit code) |
| -u          | Immediately interrupts the script when referencing a variable that is not defined previously, with the exception of $* and $@ |
| -o pipefail | Cause an interruption of the script when any command in a pipeline fails. By default the returning code of a command with pipeline is the retuning code of the last command used. |

To set the mode just declare in the beggining of the script the command set followed by the mode:

```bash
#!/bin/bash

set -euo pipefail

...
```

 

### Conditionals

Before, note that `[[ ]]` is a bash command that returns 0 (true) or 1 (false) (this is because of the retuning code in c main function)

##### Strings

| Condition                | Description      |
| ------------------------ | ---------------- |
| `[[ -z STRING ]]`        | Empty string     |
| `[[ -n STRING ]]`        | Not empty string |
| `[[ STRING == STRING ]]` | Equal            |
| `[[ STRING != STRING ]]` | Not equal        |
| `[[ STRING=~ STRING ]]`  | Regex            |

##### Numbers

| Condition           | Description           |
| ------------------- | --------------------- |
| `[[ NUM -eq NUM ]]` | Equal                 |
| `[[ NUM -ne NUM ]]` | Not equal             |
| `[[ NUM -lt NUM ]]` | Less than             |
| `[[ NUM -le NUM ]]` | Less than or equal    |
| `[[ NUM -gt NUM ]]` | Greater than          |
| `[[ NUM -ge NUM ]]` | Greater than or equal |

##### Files

| Condition               | Description                                 |
| ----------------------- | ------------------------------------------- |
| `[[ -e FILE ]]`         | FILE exists?                                |
| `[[ -r FILE ]]`         | Is FILE readable?                           |
| `[[ -h FILE ]]`         | Is FILE a symlink?                          |
| `[[ -d FILE ]]`         | Is FILE a directory?                        |
| `[[ -w FILE ]]`         | Is FILE writable?                           |
| `[[ -s FILE ]]`         | Is FILE not empty? (size of FILE > 0 bytes) |
| `[[ -f FILE ]]`         | Is FILE  a file?                            |
| `[[ -x FILE ]]`         | Is FILE executable?                         |
| `[[ FILE1 -nt FILE2 ]]` | Is FILE1 more recent than FILE2?            |
| `[[ FILE -ot FILE ]]`   | Is FILE2 more recent than FILE1?            |
| `[[ FILE -ef FILE ]]`   | Same file                                   |



### Arrays

| Bash command               | Description                                                  |
| -------------------------- | ------------------------------------------------------------ |
| `$ array=(opt1 opt2 opt3)` | Declaring an array (whie space separated)                    |
| `${array[@]}`              | All elements of the array                                    |
| `${#array[@]}`             | Number of elements                                           |
| `${!array[@]}`             | Elements keys (in case of dictionaries) or indices (in case of arrays) |
| `${array[0]}`              | Element 0                                                    |
| `${array[-1]}`             | Last element                                                 |
| `array=(${array[@]} opt4)` | Push                                                         |
| `array+=(opt4)`            | Push                                                         |
| `unset array[1]`           | Unset element 1                                              |

##### Miscelaneous 

| Command                  | Description                                     |
| ------------------------ | ----------------------------------------------- |
| `allfiles=($HOME/dir/*)` | Array of all file and dir names from $HOME/dir/ |
| `alllines=($(cat file))` | Array of all lines from file                    |



### Loops 

```bash
array=(one two three)
for element in ${array[@]}; do
	echo $element
done
```



```bash
for file in $HOME/mydir/*; do
	echo $file
done
```



### Tips

- Strict mode: 

  ```bash
  set -euo pipefail
  IFS=$'\n\t'
  ```

- Conditional

  ```bash
  if [[ -z "$STRING" ]]; then
  	echo "Empty string"
  else
  	echo "Not empty"
  fi
  ```

  ```bash
  if ping -c 1 google.com; then
  	echo "Connected"
  fi
  ```

  

- Function

  ```bash
  my_function(){
  	echo "Return this as a value"
  }
  
  $ my_function
  ```

  Alternate syntax:

  ```bash
  function my_function(){
  	echo "Return this as a value"
  }
  
  $ my_function
  ```

  

  Passing params to functions

  ```bash
  my_function(){
  	echo "Parameters passed: $1"
  }
  
  $ my_function "param"
  ```



- Always remember: In shell, return non-zero values considered false, zero value are considered true. Exemple:

  ```bash
  my_function(){
  	return 1
  }
  
  if my_function; then
  	echo "This will not be printed"
  else
  	echo "This will be printed"
  fi
  ```

  