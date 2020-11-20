# **Shell**

- [Modes](#modes)
- [Conditionals](#conditionals)
- [Loops](#loops)



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

| Condition               | Description      |
| ----------------------- | ---------------- |
| `[[ -z STRING ]]`       | Empty string     |
| `[[ -n STRING ]]`       | Not empty string |
| `[[ STRING == STRING]]` | Equal            |
| `[[ STRING != STRING]]` | Not equal        |

##### Numbers







### Loops 

How to do loops in bash

