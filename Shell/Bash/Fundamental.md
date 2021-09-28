## Variable
```bash
#!/bin/bash          
STR="Hello World!"
echo $STR

ARR1 = ("one" "two" "three")
```
## Control flow
### Iterating array
```bash
#!/bin/bash
# declare an array called array and define 3 vales
array=( one two three )
for i in "${array[@]}"
do
	echo $i
done
```

### If-else

```bash
if TEST-COMMAND1 // if [[ $VAR -gt 10 ]]
then
  STATEMENTS1
elif TEST-COMMAND2
then
  STATEMENTS2
else
  STATEMENTS3
fi
```

## Function

- `$1`, `$2`, ... `$n` will be paramter which are passed by order ($1 will be first paramter)

```bash
#!/bin/bash

greeting () {
  echo "Hello $1"
}

greeting "Joe"
```

## Logical Operators
-   `-n` `VAR` - True if the length of `VAR` is greater than zero.
-   `-z` `VAR` - True if the `VAR` is empty.
-   `STRING1 = STRING2` - True if `STRING1` and `STRING2` are equal.
-   `STRING1 != STRING2` - True if `STRING1` and `STRING2` are not equal.
-   `INTEGER1 -eq INTEGER2` - True if `INTEGER1` and `INTEGER2` are equal.
-   `INTEGER1 -gt INTEGER2` - True if `INTEGER1` is greater than `INTEGER2`.
-   `INTEGER1 -lt INTEGER2` - True if `INTEGER1` is less than `INTEGER2`.
-   `INTEGER1 -ge INTEGER2` - True if `INTEGER1` is equal or greater than INTEGER2.
-   `INTEGER1 -le INTEGER2` - True if `INTEGER1` is equal or less than `INTEGER2`.
-   `-h` `FILE` - True if the `FILE` exists and is a symbolic link.
-   `-r` `FILE` - True if the `FILE` exists and is readable.
-   `-w` `FILE` - True if the `FILE` exists and is writable.
-   `-x` `FILE` - True if the `FILE` exists and is executable.
-   `-d` `FILE` - True if the `FILE` exists and is a directory.
-   `-e` `FILE` - True if the `FILE` exists and is a file, regardless of type (node, directory, socket, etc.).



Tags: #bash, #shell


