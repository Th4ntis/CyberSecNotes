# sed, awk, and grep

Three classic text-processing tools that work beautifully together, especially in pipelines. Each does one job well, and most real-world shell one-liners are just two or three of them chained with pipes. A quick way to remember the division of labor:

* **grep** - _find_ the lines that match a pattern.
* **sed** - _edit_ a stream of text (substitute, delete, insert).
* **awk** - _process_ structured/columnar data (fields, calculations, reports).

All three read their input line by line and are commonly chained with pipes (`|`). See Common Commands > Redirection, pipes, and wildcards for the pipe and redirection basics these examples rely on.

### A note on regular expressions

grep and sed both match text with **regular expressions** (regex) - a mini language for describing patterns. The essentials:

| Pattern   | Matches                                                 |
| --------- | ------------------------------------------------------- |
| `.`       | any single character                                    |
| `*`       | zero or more of the preceding item                      |
| `^` / `$` | start / end of the line                                 |
| `[abc]`   | any one of a, b, or c; `[^abc]` = none of them          |
| `[0-9]`   | any digit (a range)                                     |
| `\`       | escapes a special character so it's literal (e.g. `\.`) |

There are two dialects. **Basic** regex (BRE) is the default in grep and sed and requires backslashes before `+`, `?`, `|`, `(`, `{`. **Extended** regex (ERE), enabled with `grep -E` or `sed -E`, treats those as special without the backslash - usually what you want when a pattern gets complicated.

### grep (Global Regular Expression Print)

Searches text for patterns (literal strings or regex) and prints the lines that match - or, with options, the non-matching lines, a count, filenames, and more.

#### Examples

```bash
# Find lines containing "error" in a file
grep "error" logfile.txt

# Case-insensitive search
grep -i "error" logfile.txt

# Show line numbers of matches
grep -n "error" logfile.txt

# Show lines that do NOT match
grep -v "error" logfile.txt

# Search recursively through a directory
grep -r "error" /var/log/

# Count how many times "TODO" appears in source files
grep -c "TODO" *.c *.h

# Use extended regex (alternation, +, ?, grouping)
grep -E "error|warning|fail" logfile.txt

# Show 3 lines of context around each match
grep -C 3 "error" logfile.txt

# Only print the matching text, not the whole line (e.g. pull out IPs)
grep -oE "[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+" access.log
```

> Common flags: `-i` ignore case, `-n` line numbers, `-v` invert match, `-r` recursive, `-c` count, `-w` whole word, `-o` only the match, `-E` extended regex, `-A`/`-B`/`-C` lines of context after/before/around.

### sed (Stream Editor)

Edits a text stream line by line - most often used for find-and-replace, but also for deleting, inserting, and printing specific lines. By default it prints the (possibly modified) stream to standard output and leaves your file untouched.

#### Examples

```bash
# Replace the FIRST occurrence of "foo" with "bar" on each line
sed 's/foo/bar/' file.txt

# Replace ALL occurrences of "foo" with "bar" on each line
sed 's/foo/bar/g' file.txt

# Case-insensitive substitution
sed 's/foo/bar/gi' file.txt

# Delete lines containing "error"
sed '/error/d' file.txt

# Print only line 5 (-n suppresses the default print)
sed -n '5p' file.txt

# Print a range of lines (10 through 20)
sed -n '10,20p' file.txt

# Edit a file IN PLACE (modifies the file directly)
sed -i 's/foo/bar/g' file.txt

# Make an in-place edit but keep a .bak backup of the original
sed -i.bak 's/foo/bar/g' file.txt

# Delete blank lines and lines starting with #
sed '/^\s*#/d;/^$/d' config.cfg

# In-place: change all tabs to four spaces in a source file
sed -i 's/\t/    /g' source.c
```

> `-i` rewrites the file in place - there is no undo, so test without `-i` first (or use `-i.bak`). The substitution syntax is `s/pattern/replacement/flags`; you can swap the delimiter when your text contains slashes, e.g. `s|/usr/local|/opt|g` - much more readable than escaping every `/`.

### awk

A pattern-scanning and processing language. It's ideal for working with columns, doing calculations, and generating reports. awk reads input line by line, splits each line into **fields** (by whitespace by default), and runs your actions when a pattern matches. Fields are referenced as `$1`, `$2`, …, and `$0` is the whole line.

The general shape is `awk 'pattern { action }'` - either part is optional. A pattern with no action prints matching lines; an action with no pattern runs on every line.

#### Examples

```bash
# Print the first column of a whitespace-separated file
awk '{print $1}' file.txt

# Print the 1st and 3rd columns
awk '{print $1, $3}' file.txt

# Print only lines where the 3rd column is greater than 100
awk '$3 > 100' file.txt

# Print lines where the 5th field > 100, showing fields 1 and 5
awk '$5 > 100 {print $1, $5}' report.log

# Sum the values in column 2 and print the total at the end
awk '{sum += $2} END {print sum}' file.txt

# Use -F to set the field delimiter (e.g. a CSV)
awk -F, '{print $1, $2}' file.csv

# Sum the third column of a CSV with a labeled total
awk -F',' '{sum += $3} END {print "Total:", sum}' sales.csv

# Print the line number and total number of fields on each line
awk '{print NR, NF, $0}' file.txt
```

> Useful built-in variables: `NR` (current record/line number), `NF` (number of fields on the line), `FS` (input field separator, set with `-F`), `OFS` (output field separator). A `BEGIN { }` block runs before any input, and `END { }` runs after all input - handy for printing headers and totals.

### Putting them together

The real payoff is chaining them. A few representative pipelines:

```bash
# Top 10 client IPs in a web log: pull the first field, sort, count, rank
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head -10

# Find TODOs across a project, strip the path noise, and number them
grep -rn "TODO" src/ | sed 's/:.*TODO/: TODO/' | nl

# Average of the second column, ignoring comment lines
grep -v '^#' data.txt | awk '{sum+=$2; n++} END {print sum/n}'
```

`sort` and `uniq -c` aren't part of this trio, but they show up constantly alongside it - `sort | uniq -c | sort -rn` is the canonical "count and rank" idiom.
