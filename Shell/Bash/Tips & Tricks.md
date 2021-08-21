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

Tags: #bash, #shell