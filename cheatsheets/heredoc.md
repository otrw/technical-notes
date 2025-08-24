# Cheatsheet: Here Documents (Heredoc)

Instructions for creating multi-line content in new and existing files.

## Basics

```bash
command <<EOF
text line 1
text line 2
EOF
```

- Passes multiple lines as **stdin** to a command.
- `EOF` can be any marker word.
- Must appear at start of line with no leading spaces.


## Variable Expansion

```bash
# Expands variables and command subs
cat <<EOF
Hello $USER, today is $(date)
EOF

# No expansion (literal text)
cat <<'EOF'
Hello $USER, today is $(date)
EOF
```

## File Redirection

```bash
# Overwrite file
cat <<EOF > file.txt
content
EOF

# Append to file
cat <<EOF >> file.txt
more content
EOF
```

## Editing Protected Files

**Option 1 – using `tee`**

```bash
cat <<EOF | sudo tee -a /etc/dnf/dnf.conf >/dev/null
fastestmirror=True
max_parallel_downloads=10
EOF
```

**Option 2 – using `sh -c`**

```bash
sudo sh -c 'cat <<EOF >> /etc/dnf/dnf.conf
fastestmirror=True
max_parallel_downloads=10
EOF'
```

---

## Safety Tip

Always back up config files before appending:

```bash
sudo cp /etc/dnf/dnf.conf{,.bak.$(date +%F)}
```

---

## Additional Notes

- **Redirection happens in the current shell**  
    `sudo cat <<EOF >> /etc/file` fails because `>>` is done by your non-root shell. Use `sudo sh -c '… >> /etc/file'` or `| sudo tee -a /etc/file`.
    
- **Delimiter must be flush-left**  
    The closing `EOF` (or your marker) must start in column 1 with **no spaces** before it.
    
- **Quoted delimiter disables expansion**  
    `<<'EOF'` makes the content literal: **no** `$VAR`, `$(cmd)`, or backslash escapes.
    
- **Unquoted delimiter expands**  
    With `<<EOF`, shell expands `$VAR`, `$(cmd)`, backslashes, and `$(< file)` if supported. Be careful pasting untrusted text.
    
- **Use `<<-` to allow indentation with tabs only**  
    `<<-EOF` strips **leading TABs** (not spaces) from each line and the closing marker. Handy for indenting in scripts.
    
- **A newline before the closing delimiter is required**  
    The heredoc ends only when a line exactly matches the delimiter. Trailing spaces on that line will break it.
    
- **Pick a unique delimiter**  
    If your content contains `EOF`, choose something unlikely, e.g. `__DNF_CONF__`.
    
- **Line endings matter**  
    Pasting Windows CRLF can cause weirdness in config files. Convert if needed: `dos2unix`.
    
- **`tee` echoes to stdout**  
    When using `tee`, silence it if you don’t want output in the terminal: `| sudo tee -a /path >/dev/null`.
    
- **Here-doc vs here-string**  
    `<<< "text"` is a _here-string_ (single line). Multiline blocks need a heredoc.
    
- **Signals & `set -e`**  
    A command reading a heredoc that exits non-zero will still have consumed the block. Use clear error checks after the command.
    
- **File descriptors**  
    You can target FDs directly:
    
    ```bash
    cat <<EOF 1>out.log 2>err.log
    …
    EOF
    ```
    
- **Binary-ish content**  
    Heredocs are text-oriented. For binary data, prefer files or base64 within the heredoc then decode.
