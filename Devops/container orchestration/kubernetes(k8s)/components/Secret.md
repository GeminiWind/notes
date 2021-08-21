# Secret 

Used to store smaill amount info like token, password

## Create secret

A `Secret` can contain user credentials required by pods to access a database. For example, a database connection string consists of a username and password. You can store the username in a file `./username.txt` and the password in a file `./password.txt` on your local machine.

```shell
echo -n 'admin' > ./username.txt
echo -n '1f2d1e2e67df' > ./password.txt
```

In these commands, the `-n` flag ensures that the generated files do not have an extra newline character at the end of the text. This is important because when `kubectl` reads a file and encodes the content into a base64 string, the extra newline character gets encoded too.

The `kubectl create secret` command packages these files into a Secret and creates the object on the API server.

```shell
kubectl create secret generic db-user-pass \
  --from-file=./username.txt \
  --from-file=./password.txt
```

The output is similar to:

```
secret/db-user-pass created
```

The default key name is the filename. You can optionally set the key name using `--from-file=[key=]source`. For example:

```shell
kubectl create secret generic db-user-pass \
  --from-file=username=./username.txt \
  --from-file=password=./password.txt
```

## Decoding secret

To view the contents of the Secret you created, run the following command:

```shell
kubectl get secret db-user-pass -o jsonpath='{.data}'
```

The output is similar to:

```json
{"password":"MWYyZDFlMmU2N2Rm","username":"YWRtaW4="}
```

Now you can decode the `password` data:

```shell
echo 'MWYyZDFlMmU2N2Rm' | base64 --decode
```

The output is similar to:

```
1f2d1e2e67df
```