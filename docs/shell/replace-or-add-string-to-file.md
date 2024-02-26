# Replace or Add a String to File

```
grep -q string file && 
    sed -i 's/string/newstring/' file || echo "newstring" >> file
```

The above is a shorthand way of writing:

```
if grep -q string file; then 
    sed -i 's/string/newstring/' file
else
    echo "newstring" >> file
fi
```
