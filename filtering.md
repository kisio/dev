## Filtering Output and Finding Things

### 1. Logical AND (`&&`)

*   **Purpose:** Executes the second command *only if* the first command succeeds (returns an exit status of 0).
*   **Syntax:** `command1 && command2`
*   **Functionality:** Useful for creating conditional sequences of commands.
*   **Example:**
    *   Create a directory, then change into it, only if creation was successful:
        ```bash
        mkdir my_project && cd my_project
        ```
        `

### 2. `cut`

*   **Purpose:** Extracts sections from each line of files or standard input.
*   **Key Options:**
    *   `-d DELIM`: Specifies the field delimiter (e.g., `-d:`, `-d,`). Default is tab.
    *   `-f FIELD_LIST`: Selects fields. Can be a single number (e.g., `-f1`), a range (e.g., `-f1-3`), or a comma-separated list (e.g., `-f1,5`).
*   **Example:**
    *   Display usernames from `/etc/passwd` (first field, colon-separated):
        ```bash
        cut -d: -f1 /etc/passwd
        ```
        `
    *   Display username and home directory:
        ```bash
        cut -d: -f1,6 /etc/passwd
        ```
        `

### 3. `sort`

*   **Purpose:** Sorts lines of text files or standard input.
*   **Key Options:**
    *   `-r`: Reverse the result of comparisons.
    *   `-n`: Compare according to numerical value.
    *   `-k FIELD`: Sort by a specific field (e.g., `-k2` for the second field).
    *   `-u`: With `-c`, check for strict ordering; without `-c`, output only the first of an equal run.
*   **Example:**
    *   Sort a list of names alphabetically:
        ```bash
        cat names.txt | sort
        ```
        `
    *   Sort numbers numerically in reverse order:
        ```bash
        echo -e "10\n1\n5" | sort -nr
        ```
        `

### 4. `uniq`

*   **Purpose:** Reports or filters out repeated lines in a file. **Important:** `uniq` only detects adjacent duplicate lines. You usually need to `sort` first.
*   **Key Options:**
    *   `-c`: Precede lines by count of occurrences.
    *   `-d`: Only print duplicate lines.
    *   `-u`: Only print unique lines.
*   **Example:**
    *   Count unique words in a file (after lowercasing and sorting):
        ```bash
        cat document.txt | tr ' ' '\n' | tr '[:upper:]' '[:lower:]' | sort | uniq -c | sort -nr
        ```
        `

### 5. `wc` (Word Count)

*   **Purpose:** Prints newline, word, and byte counts for files.
*   **Key Options:**
    *   `-l`: Print the newline counts (lines).
    *   `-w`: Print the word counts.
    *   `-c`: Print the byte counts.
    *   `-m`: Print the character counts.
*   **Example:**
    *   Count lines in a file:
        ```bash
        wc -l my_log.txt
        ```
        `
    *   Count words from command output:
        ```bash
        ls -l | wc -w
        ```
        `

### 6. `grep` (Global Regular Expression Print)

*   **Purpose:** Searches for patterns in files or standard input. It's incredibly powerful due to its use of regular expressions.
*   **Key Options:**
    *   `-i`: Ignore case distinctions.
    *   `-v`: Invert the sense of matching, i.e., select non-matching lines.
    *   `-r` or `-R`: Search directories recursively.
    *   `-n`: Display line number with output.
    *   `-c`: Print only a count of matching lines per file.
    *   `-l`: Print only the names of files that contain matches.
    *   `-w`: Select only those lines containing matches that form whole words.
*   **Example:**
    *   Find lines containing "error" in `syslog`:
        ```bash
        grep "error" /var/log/syslog
        ```
        `
    *   Find lines NOT containing "bash" in `/etc/passwd`:
        ```bash
        grep -v "bash" /etc/passwd
        ```
        `
    *   Find all `.conf` files in `/etc` that contain the word "server", ignoring case:
        ```bash
        grep -Ri "server" /etc/*.conf
        ```
        `
