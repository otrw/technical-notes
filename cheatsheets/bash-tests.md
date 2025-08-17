# Bash Tests - Expression Cheatsheet

## String Tests

| Test           | Meaning             | Example                 |
| -------------- | ------------------- | ----------------------- |
| `-z "$var"`    | String is empty     | `[ -z "$input" ]`       |
| `-n "$var"`    | String is not empty | `[ -n "$name" ]`        |
| `"$a" = "$b"`  | Strings are equal   | `[ "$user" = "admin" ]` |
| `"$a" != "$b"` | Strings not equal   | `[ "$os" != "linux" ]`  |

---
## Integer Tests

| Test  | Meaning          | Example                |
| ----- | ---------------- | ---------------------- |
| `-eq` | Equal            | `[ "$x" -eq 5 ]`       |
| `-ne` | Not equal        | `[ "$x" -ne 0 ]`       |
| `-gt` | Greater than     | `[ "$age" -gt 18 ]`    |
| `-lt` | Less than        | `[ "$count" -lt 100 ]` |
| `-ge` | Greater or equal | `[ "$n" -ge 1 ]`       |
| `-le` | Less or equal    | `[ "$n" -le 10 ]`      |

---
## File Tests

| Test         | Meaning                 | Example                   |
| ------------ | ----------------------- | ------------------------- |
| `-f "$file"` | File exists             | `[ -f ~/.bashrc ]`        |
| `-d "$dir"`  | Directory exists        | `[ -d /etc/nginx ]`       |
| `-e "$path"` | File or dir exists      | `[ -e "$HOME/.profile" ]` |
| `-s "$file"` | File exists & not empty | `[ -s log.txt ]`          |
| `-r "$file"` | Readable file           | `[ -r config.yaml ]`      |
| `-w "$file"` | Writable file           | `[ -w output.txt ]`       |
| `-x "$file"` | Executable file         | `[ -x script.sh ]`        |

---
## Logic & Grouping

| Symbol      | Meaning       | Example                                        |
| ----------- | ------------- | ---------------------------------------------- |
| `!`         | NOT           | `[ ! -f "$file" ]`                             |
| `-a`        | AND           | `[ "$x" -gt 0 -a "$x" -lt 10 ]`                |
| `-o`        | OR            | `[ "$x" -lt 0 -o "$x" -gt 100 ]`               |
| `[[ ... ]]` | Extended test | `[[ "$a" == "$b" && -f "$file" ]]` (bash only) |

---

## Tips

* **Quote variables**: Always write `"$var"` in tests.  
  * Prevents **word splitting** (spaces → multiple words) and **globbing** (`*`, `?` → filename matches).  
  ```bash
  var="hello world"
  [ "$var" = "hello world" ]   # safe
  [ $var = "hello world" ]     # error (splits into 2 words)
  ```

* **Prefer `[[ ... ]]` over `[ ... ]`**:  
  * `[[ ... ]]` is a Bash keyword, safer and more powerful than `[ ... ]` (POSIX command).  
  * No unwanted splitting/globbing inside.  
  * Supports regex (`=~`) and `&&` / `||` directly.  
  ```bash
  [[ $var = "hello world" ]]       # works without quoting
  [[ $var =~ ^hello ]]             # regex match
  [[ $x -gt 5 && $x -lt 10 ]]      # multiple conditions
  ```

* **Use `-n` / `-z` for string checks**:  
  ```bash
  [[ -n $str ]]   # non-empty
  [[ -z $str ]]   # empty
  ```

* **File tests**: `-e` (exists), `-f` (regular file), `-d` (directory).  
  ```bash
  [[ -f file.txt ]] && echo "Regular file"
  [[ -d /etc ]]    && echo "Directory"
  ```

* **Arithmetic with `(( ... ))`**:  
  ```bash
  (( x > 5 && x < 10 )) && echo "x in range"
  ```

* **Quick one-liners with `&&` / `||`**:  
  ```bash
  [[ -f config ]] && source config || echo "No config found"
  ```

* **Use `case` for multiple options**:  
  ```bash
  case $answer in
    y|Y) echo "yes" ;;
    n|N) echo "no" ;;
    *)   echo "invalid" ;;
  esac
  ```

---
## Example: file check

```bash
if [ -f "$config" ] && [ -r "$config" ]; then
  echo "Config is ready"
else
  echo "Missing or unreadable config"
fi
```

## Example: Exit Status (`$?`)
```bash
somecommand
if [ $? -ne 0 ]; then
  echo "Command failed"
fi
````
- `$?` is the exit status of the last command.  
- `0` = success, anything else = error/failure.
