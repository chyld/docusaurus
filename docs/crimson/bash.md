---
sidebar_position: 3
---

# Bash Scripting

## Variables

```bash
var1="$abc"
var2="${var1}_part2"
```

- creating variables
- no space between variable and value
- use double quotes around variables
- use `${var}` when you want to string concatenation

```bash
var1="hello"
export var2="world"
```

- a shell variable
- an environment variable

## Arguments

```bash
$0, $1, $2, $@, $*
```

- arguments, with `$0` being the filenaem
- `$@` is an array of all arguments minus `$0`
- `$*` is one string with all arguments

## Quotes

```bash
' vs "
```

- single quotes will not expand
- double quotes will expand

## Brace Expansion

```bash
touch file.{txt,svg,png}      # file.txt, file.svg, etc
touch file_{1..5}             # file_1, file_2, etc
touch file_{a..z}             # file_a, file_b, etc
touch file_{a..c}{1..3}.txt   # file_a1, file_a2, file_a3, etc
touch file_{0001..20}         # file_0001, file_0002, etc
cp orig.txt{,.bak}            # cp orig.txt orig.txt.bak
```

## Braces

```bash
{ ls; pwd; ps }
```

- grouping commands
- runs in **current process**
- does not capture output
- **needs space** at beginning and end

```bash
(ls; pwd; ps)
```

- grouping commands
- runs in a **subshell**
- does not capture output
- no extra space needed

```bash
var=$(ls;pwd;uname -a;cat doc.txt)
```

- runs commands in a **subshell**
- **captures** output from **all** commands into variable

```bash
${#var}
```

- get the length of var

```bash
${string//search/replace}
${dogcathorse//dog/pup}
```

- search and replace parts of a string

```bash
${var:-$var2}
```

- default value for var if it does not exist

```bash
${var#pattern}
${var%pattern}
```

- remove the prefix/suffix pattern from var

```bash
${var:offset:length}
```

- get a substring of var

```bash
var=(1 2 3)
```

- create an **array**
- able to loop over

## Redirects

```bash
echo "hello" 1> out.txt         # stdout
echo "world" 1>> out.txt        # append to stdout
echo "world" 2> err.txt         # stderr
echo "junk" 1> /dev/null 2>&1   # stderr (2) is sent to same location as stdout (1)
diff <(ls /docs) <(ls /bak)     # packages 2 stdouts into files used as input into diff
cat <(ls) 1> out.txt 2> err.txt # full example
```

- if you have a program, like cat, that needs a file, use `<(cmd)` and it will package the results as a file

## Conditionals

```bash
[[ -z STRING ]]           # Empty string
[[ -n STRING ]]           # Not empty string
[[ STRING == STRING ]]    # Equal
[[ STRING != STRING ]]    # Not Equal
[[ STRING =~ STRING ]]    # Regexp

[[ NUM -eq NUM ]]         # Equal
[[ NUM -ne NUM ]]         # Not equal
[[ NUM -lt NUM ]]         # Less than
[[ NUM -le NUM ]]         # Less than or equal
[[ NUM -gt NUM ]]         # Greater than
[[ NUM -ge NUM ]]         # Greater than or equal

[[ -e FILE ]]             # Exists
[[ -r FILE ]]             # Readable
[[ -h FILE ]]             # Symlink
[[ -d FILE ]]             # Directory
[[ -w FILE ]]             # Writable
[[ -s FILE ]]             # Size is > 0 bytes
[[ -f FILE ]]             # File
[[ -x FILE ]]             # Executable
```

## Loops

```bash
# loop over words

for name in Alice Bob Charlie; do
  echo "Hello, $name!"
done
```

```bash
# loop over array

fruits=(Apple Banana Cherry)
for fruit in $fruits; do
  echo "Fruit: $fruit"
done
```

```bash
# loop over number range

for i in {1..5}; do
  echo "Number $i"
done
```

```bash
# loop over files in a directory

for file in $(pwd)/*.md; do
  echo "file: $file"
done
```

```bash
# loop forever, and ever

while true; do
done
```

## Functions

```bash
my_func() {
    local var1
    var1="$1"
    return 0
}
```

- the function definition
- use `local` to declare variables
- assign variable should be separate from declaration
- return 0 is success, greater than 1 is failure

## Globs

```bash
*
?
[abc]
```

- bash expands globs to match filenames
- matches 0 or more characters
- matches 1 character
- matches either `a`, `b` or `c`

## Traps

`trap COMMAND EVENT`

- trap will listen for an event and then trigger the command
- useful for resource cleanup

## Errors

- `set -e` stops the script on errors
- `set -u` stops the script if you try to use an unset variable
- `set -o pipefail` stops the script if any command in a pipeline fails
- `set -euo pipefail` puts them all together

## Debugging

```bash
set -x
```

- put at top of bash script
- great for debugging

```bash
shellcheck script.sh
```

- checks for syntax errors

## Miscellaneous

```bash
bash script.sh
source script.sh
```

- `bash` runs the script in a subshell
- `source` runs the script in the current process
