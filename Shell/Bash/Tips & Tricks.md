# Tips & Tricks

## Adding new line to end of file 
```bash
echo "" >> file.txt
```

## Creating a new file with echo
```bash
echo "Some line" > file1.txt
```

## Creating a new file with heredoc

```bash
cat << EOF > file1.txt
```

## Pipe command
```bash
find -f *.txt | grep "keyword"
```

## Using `xargs`

```bash
find . -type d -name "*log*" | xargs -I {} sh -c "ls -ltr | tail -10"
```

## Base-64 encoding

```bash
echo 'linuxhint.com' | base64
```

## Base-64 decoding

```bash
echo 'bGludXhoaW50LmNvbQo=' | base64 --decode
```


## Importing function from another bash file

**script**
```bash
foo ()    { echo "foo()"; }

bar ()    { echo "bar()"; }

script () {
  ARG1=$1
  ARG2=$2
  #
  echo "Running '$RUNNING'..."
  echo "script() - all args:  $@"
  echo "script() -     ARG1:  $ARG1"
  echo "script() -     ARG2:  $ARG2"
  #
  foo
  bar
}

RUNNING="$(basename $0)"

if [[ "$RUNNING" == "script" ]]
then
  script "$@"
fi
```

**runtests**

```bash
#!/bin/bash

source script 

# execute 'script' function in sourced file 'script'
script arg1 arg2 arg3
```

## Parsing args into bash shell file

```bash
./hello.sh hai 38years
```

## Parsing argument into bash file with bash space-separated (e.g., `--option argument`)


```bash
#!/bin/bash

POSITIONAL=()
while [[ $# -gt 0 ]]; do
  key="$1"

  case $key in
    -e|--extension)
      EXTENSION="$2"
      shift # past argument
      shift # past value
      ;;
    -s|--searchpath)
      SEARCHPATH="$2"
      shift # past argument
      shift # past value
      ;;
    -l|--lib)
      LIBPATH="$2"
      shift # past argument
      shift # past value
      ;;
    --default)
      DEFAULT=YES
      shift # past argument
      ;;
    *)    # unknown option
      POSITIONAL+=("$1") # save it in an array for later
      shift # past argument
      ;;
  esac
done

set -- "${POSITIONAL[@]}" # restore positional parameters

echo "FILE EXTENSION  = ${EXTENSION}"
echo "SEARCH PATH     = ${SEARCHPATH}"
echo "LIBRARY PATH    = ${LIBPATH}"
echo "DEFAULT         = ${DEFAULT}"
echo "Number files in SEARCH PATH with EXTENSION:" $(ls -1 "${SEARCHPATH}"/*."${EXTENSION}" | wc -l)
if [[ -n $1 ]]; then
    echo "Last line of file specified as non-opt/last argument:"
    tail -1 "$1"
fi
```


## Shortcuts

|Shorcut| What is it|
|:--:|:--:|
|`Ctrl` + `X` + `E`| temporary editor for current command (your editor is set by `$EDITOR`)|
|`Ctrl` + `K`| copy text after cursor|
|`Ctrl` + `U`| copy text before cursor|
| `Ctrl` + `Y`| yarn the text|
| `sudo!!`| re-run previous command with 'sudo' prepended|
| `cd -`| go to previous current working directory (`$pwd`)|
|`Ctrl` + `R` => type your pattern to search command|Search matching history command (like `zsh-auto-completion`)|



Tags: #bash, #shell