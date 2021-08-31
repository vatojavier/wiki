# Useful Bash commands

## sed
### Change files content 
```bash
sed -i 's/search_string/replace_string/' filenames
```

**‘-i’** option is used to modify the content of the original file with the replacement string if the search string exists in the file.

**‘s’** indicates the substitute command.
