## Shell Features - Pipes and Redirection

**1. Pipes (`|`)**

*   **Purpose:** Connects the standard output (stdout) of one command to the standard input (stdin) of another command.
*   **Syntax:** `command1 | command2`
*   **Functionality:** Allows complex operations by chaining multiple simple commands. `command2` receives the processed output of `command1`.
*   **Example:**
    *   List files in a directory and then count them:
        ```bash
        ls -l | wc -l
        ```
        `ls -l` outputs a long listing of files, `wc -l` then counts the lines (which correspond to files/directories).
    *   Find a specific process and display its details:
        ```bash
        ps aux | grep firefox
        ```
        `ps aux` lists all running processes, `grep firefox` filters those lines that contain "firefox".

**2. Redirection**

*   **Purpose:** Controls where a command's input comes from or where its output goes.
*   **File Descriptors (FDs):**
    *   `0`: Standard Input (stdin) - Default source is keyboard.
    *   `1`: Standard Output (stdout) - Default destination is screen.
    *   `2`: Standard Error (stderr) - Default destination is screen.

### 2.1 Output Redirection

*   **Overwrite (`>`):** Redirects stdout to a file, overwriting its contents if it exists.
    *   **Syntax:** `command > file.txt`
    *   **Example:**
        ```bash
        echo "Hello world" > greeting.txt
        ```
        Creates `greeting.txt` with "Hello world". If `greeting.txt` existed, its content is replaced.
        
        `
*   **Append (`>>`):** Redirects stdout to a file, appending to its contents if it exists. If the file doesn't exist, it's created.
    *   **Syntax:** `command >> file.txt`
    *   **Example:**
        ```bash
        echo "How are you?" >> greeting.txt
        ```
        Adds "How are you?" to the end of `greeting.txt`.
        
        `
*   **Redirect stderr (`2>`):** Redirects standard error to a file.
    *   **Syntax:** `command 2> error.log`
    *   **Example:**
        ```bash
        ls non_existent_file 2> errors.txt
        ```
        The error message for `non_existent_file` is written to `errors.txt` instead of the screen.
        
        `
*   **Redirect both stdout and stderr:**
    *   **To separate files:** `command > output.txt 2> errors.txt`
    *   **To the same file (legacy):** `command > all_output.txt 2>&1`
        *   `2>&1` means "redirect file descriptor 2 (stderr) to the same place as file descriptor 1 (stdout)". This order is important.
    *   **To the same file (bash shorthand):** `command &> all_output.txt` or `command >& all_output.txt`
    *   **Example:**
        ```bash
        find /etc -name "*.conf" > found_configs.txt 2> find_errors.txt
        ```
        `
        ```bash
        find /etc -name "*.conf" &> all_find_output.txt
        ```
        `

### 2.2 Input Redirection (`<`)

*   **Purpose:** Changes stdin from the keyboard to a specified file.
*   **Syntax:** `command < file.txt`
*   **Functionality:** The command reads its input from `file.txt` instead of waiting for keyboard input.
*   **Example:**
    *   Count lines in a file using `wc -l`:
        ```bash
        wc -l < greeting.txt
        ```
        `wc -l` now reads `greeting.txt` as its input.
        
        `

### 2.3 Here Strings (`<<<`) and Here Documents (`<<`)

*   **Here String (`<<<`):** Provides a single string as input to a command.
    *   **Syntax:** `command <<< "string"`
    *   **Example:**
        ```bash
        grep "world" <<< "Hello world"
        ```
        `grep` searches for "world" within the literal string "Hello world".
        
        `
*   **Here Document (`<<`):** Provides multiple lines of input to a command until a specified delimiter is encountered.
    *   **Syntax:**
        ```bash
        command << DELIMITER
        line 1
        line 2
        ...
        DELIMITER
        ```
    *   **Example:**
        ```bash
        cat << EOF
        This is line one.
        This is line two.
        EOF
        ```
        `cat` reads the two lines as input and prints them to the screen.
        
        `
