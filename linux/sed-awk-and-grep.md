# Sed Awk and Grep

## **grep (Global Regular Expression Print)**

Searches text for patterns (strings or regex), most often used for finding lines that match (or don’t match) a pattern. Searches input for lines that match a regular expression and prints those lines (or optionally the count, filenames, etc.).

#### Examples:

```
# Find lines containing "error" in a file
grep "error" logfile.txt

# Case-insensitive search
grep -i "error" logfile.txt

# Show line numbers of matches
grep -n "error" logfile.txt

# Show lines that do NOT match
grep -v "error" logfile.txt

# Show all lines containing the word "error" (case‑insensitive) in a log file
grep -i "error" /var/log/syslog

# Count how many times "TODO" appears in source files
grep -c "TODO" *.c *.h
```

## sed (Stream Editor)

Edits text streams, mostly used for substitution, deletion, insertion, of strings within files. Reads a stream line‑by‑line, applies editing commands (substitutions, deletions, insertions, etc.), and writes the result.

#### Examples

```
# Replace first occurrence of "foo" with "bar" on each line
sed 's/foo/bar/' file.txt

# Replace ALL occurrences of "foo" with "bar"
sed 's/foo/bar/g' file.txt

# Delete lines containing "error"
sed '/error/d' file.txt

# Print only line 5
sed -n '5p' file.txt

# Edit file in-place
sed -i 's/foo/bar/g' file.txt

# Replace the first occurrence of "foo" with "bar" on each line
sed 's/foo/bar/' file.txt

# Delete blank lines and lines starting with #
sed '/^\s*#/d;/^$/d' config.cfg

# In‑place edit: change all tabs to four spaces in a source file
sed -i 's/\t/    /g' source.c
```

## AWK

Pattern scanning and processing language. Mostly used for working with structured data (columns), calculations, reports. Scans input line‑by‑line, splits each line into fields (default whitespace), and executes user‑defined actions when patterns match.

#### Examples

```
# Print first column of a space-separated file
awk '{print $1}' file.txt

# Print 1st and 3rd columns (tab or space separated)
awk '{print $1, $3}' file.txt

# Print lines where 3rd column > 100
awk '$3 > 100' file.txt

# Calculate sum of values in column 2
awk '{sum += $2} END {print sum}' file.txt

# Use -F to specify delimiter (e.g., CSV)
awk -F, '{print $1,$2}' file.csv

# Print the second column of a space‑separated file
awk '{print $2}' data.txt

# Sum the values in the third column of a CSV (comma as FS)
awk -F',' '{sum += $3} END {print "Total:", sum}' sales.csv

# Show lines where the 5th field > 100 and print fields 1 and 5
awk '$5 > 100 {print $1, $5}' report.log
```
