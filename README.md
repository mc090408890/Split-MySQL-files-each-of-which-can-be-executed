# MySQL Dump Splitter

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub last commit](https://img.shields.io/github/last-commit/yourusername/your-repo-name)](https://github.com/yourusername/your-repo-name/commits/main)

## Overview

This project provides a robust solution for splitting large MySQL dump files (`.sql` files) into smaller, manageable, and **independently executable** parts. This is particularly useful when dealing with import size limits imposed by tools like phpMyAdmin or when you need to import specific sections of a large database dump.

Unlike simple byte-based file splitting, this solution ensures that each generated `.sql` file contains complete and valid SQL statements, preventing truncated or broken commands that would lead to import errors.

## Features

* **Intelligent SQL Parsing:** Splits files at logical SQL statement boundaries (e.g., after a complete `INSERT` statement, `CREATE TABLE`, `ALTER TABLE`, etc.) to ensure each output file is valid and executable.
* **Configurable Output Size:** Allows you to specify a maximum size for each split file (e.g., 10MB, 50MB), making it ideal for bypassing upload limits.
* **Independent Executability:** Each split file includes necessary header information (like `SET` commands, character set declarations) to allow for independent import without dependencies on other split files.
* **Error Handling:** Basic error checking for file operations.

## How It Works (Conceptual)

The core logic involves reading the large SQL dump file, buffering SQL statements until a complete statement is identified (typically delimited by a semicolon), and then writing these statements to a new output file. Before writing a new statement, the script checks if adding it would exceed the specified maximum file size. If it does, a new output file is started.

## Getting Started

### Prerequisites

* PHP 7.4 or higher (if using the PHP script).
* Access to a command-line interface.

### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/mc090408890/Split-MySQL-files-each-of-which-can-be-executed.git
    cd your-repo-name
    ```

2.  **Place your MySQL dump file:**
    Copy your large MySQL dump file (e.g., `my_large_database.sql`) into the project directory or specify its full path in the configuration.

### Usage

1.  **Configure the script (if applicable):**
    Open the main script file (e.g., `split_dump.php` or similar) and modify the following variables:
    * `$inputFile`: Path to your large MySQL dump file.
    * `$outputDir`: Directory where the split files will be saved.
    * `$maxFileSize`: The desired maximum size for each split file (e.g., `10 * 1024 * 1024` for 10MB).

2.  **Run the script:**
    Execute the PHP script from your terminal:
    ```bash
    php split_dump.php
    ```

    Or, if using a standalone executable tool, follow its specific instructions.

3.  **Import the split files:**
    Once the splitting process is complete, you will find the smaller `.sql` files in the specified output directory (e.g., `split_dumps/`). You can then import these files individually using tools like phpMyAdmin, MySQL Workbench, or the `mysql` command-line client:

    ```bash
    mysql -u your_username -p your_database_name < path/to/split_dumps/dump_part_001.sql
    mysql -u your_username -p your_database_name < path/to/split_dumps/dump_part_002.sql
    # ... and so on for each part
    ```

## Contributing

Contributions are welcome! If you have suggestions for improvements, new features, or bug fixes, please open an issue or submit a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

If you have any questions or need assistance, feel free to open an issue on GitHub.

---