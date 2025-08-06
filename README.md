<p align="center">
  <img src="./assets/avatar.jpeg" alt="Project File Concatenator Avatar" width="200">
</p>

# Project File Concatenator

This repository contains a powerful and configurable Bash script that traverses a project directory, filters files based on various criteria, and concatenates their contents into a single text file.

## Overview

The main purpose of this script is to consolidate an entire software project's source code into a single, well-formatted file. This is particularly useful for feeding a complete codebase into a Large Language Model (LLM) or AI assistant for tasks such as:

*   **Holistic Debugging:** Providing the AI with the full context of all relevant files to find complex bugs.
*   **Code Analysis & Refactoring:** Asking for suggestions on improving code quality, structure, or performance.
*   **Generating Documentation:** Allowing the AI to understand the entire project to create comprehensive documentation.
*   **Onboarding:** Creating a single file that a new developer (or AI) can review to quickly understand the project architecture.

The script is highly customizable, allowing you to exclude irrelevant files, directories, and even specific lines of code (like comments or empty lines) to create a clean and focused output.

### Features

*   **Recursive File Traversal:** Scans the entire input directory and its subdirectories.
*   **Flexible Exclusion Rules:** Exclude directories, files, and file extensions using simple `.csv` configuration files with glob pattern support.
*   **Content Filtering:** Automatically remove empty lines and comment lines from the source files.
*   **Custom Comment Signs:** Define your own comment indicators (e.g., `#`, `//`, `--`) in a configuration file.
*   **Smart File Skipping:** Option to skip files that become empty after filtering.
*   **Detailed Logging:** Creates a log file (`concat_files.log`) to record all actions, exclusions, and errors.
*   **Included Files List:** Generates a sorted list (`included_files.txt`) of all files that were added to the final output.
*   **Pure Bash:** Runs in any modern Linux/Unix environment with no external dependencies beyond standard core utilities (`find`, `grep`, `sed`).

## Prerequisites

*   A Unix-like operating system (e.g., Ubuntu 24.04, macOS).
*   Bash (Bourne-Again SHell).
*   Standard command-line utilities: `find`, `grep`, `sed`, `realpath`, `mktemp`.

## Setup & Configuration

1.  **Save the Script:**
    Save the main script as `concatenator.sh`.

2.  **Make it Executable:**
    Open your terminal and grant execute permissions to the script:
    ```bash
    chmod +x concatenator.sh
    ```

3.  **Configure the Script:**
    Open `concatenator.sh` and edit the variables in the **User Configuration** section at the top. You can set the input directory, output file paths, and filtering behavior here.

    ```bash
    # 1. Core Paths
    INPUT_DIRECTORY="../my_project/"
    OUTPUT_FILE="./output/concatenated_output.txt"
    # ... and other settings
    ```

4.  **Create Configuration Files:**
    In the same directory as the script, create the following plain text files to define your exclusion rules. You can use the provided `.example` files as templates.

    *   **`exclude_directories.csv`**: List directory names or paths to exclude.
        ```
        .git/
        node_modules/
        .venv/
        __pycache__/
        ```

    *   **`exclude_files.csv`**: List file names or paths to exclude. Glob patterns are supported.
        ```
        *.log
        .env
        package-lock.json
        ```

    *   **`exclude_extensions.csv`**: List file extensions to exclude (the leading dot is optional).
        ```
        .tmp
        .bak
        .swp
        ```

    *   **`comment_signs.csv`**: List the strings that start a comment line.
        ```
        #
        //
        --
        ```

## How to Run

With the configuration in place, simply execute the script from your terminal:

```bash
./concatenator.sh
```

The script will start the process and print a confirmation message upon completion.

### Output Files

After running, you will find the following generated files:

*   **`concatenated_output.txt`** (or your custom `OUTPUT_FILE`): The final combined file. Each included file's content is wrapped in a Markdown code block, with its relative path in the header.
    ```
    ```path/to/file1.py
    print("Hello, World!")
    ```
    ```path/to/another/file.js
    console.log("Hello again!");
    ```
    ```

*   **`included_files.txt`**: A sorted list of the full paths of all files included in the concatenation.
*   **`concat_files.log`**: A detailed log of the script's execution, including all exclusions and operations. Check this file for troubleshooting.

## Project Structure

```
.
├── concatenator.sh                 # The main executable script
├── exclude_directories.csv         # Rule: Exclude directories matching these patterns
├── exclude_files.csv               # Rule: Exclude files matching these patterns
├── exclude_extensions.csv          # Rule: Exclude files with these extensions
├── comment_signs.csv               # Rule: Lines starting with these are comments
├── output/
│   ├── concatenated_output.txt     # The final merged file
│   ├── included_files.txt          # List of all files included in the output
│   └── concat_files.log            # Log of the script's operations
└── README.md                       # This file
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---
*Authored by Reza 'Sam' Aghamohammadi (Hacknitive)*