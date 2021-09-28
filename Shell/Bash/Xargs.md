# xargs

## Using `xargs`

```bash
find . -type d -name "*log*" | xargs -I {} sh -c "ls -ltr | tail -10"
```