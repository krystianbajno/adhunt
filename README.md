# ADHUNT

**ADHUNT** is a versatile polyglot file (Bash, PowerShell, Python, HTML) for gathering domain information. It works everywhere without requiring installation. You can open the website and hit save as or you can run it in memory

### Collectors:

- **PowerShell**: `New-Object DirectoryServices.DirectorySearcher`
- **Bash**: `ldapsearch`

### Converters:

- **Python**: Converts `ldapsearch` LDIF results into JSON.

### GUI:

- **HTML**: Runs directly in your browser.

## Usage Scenarios:

### PowerShell
Run the HTML file as a PowerShell script to dump domain information (users, groups, computers, and group policies):
- From a local file:
  ```powershell
  iex(gc -path adhunt.html -raw)
  ```
- Download and execute in memory:
  ```powershell
  iwr https://adhunt.netlify.app | iex
  ```

### Bash
Run the HTML file as a Bash script to dump domain information (requires `ldapsearch`):
- Provide credentials:
  ```bash
  bash adhunt.html <server> <domain> <user> <password>
  ```
- Prompt for credentials:
  ```bash
  bash adhunt.html
  ```
- Download and execute in memory:
  ```bash
  curl https://adhunt.netlify.app | bash
  ```

### Python
Parse LDIF `ldapsearch` results into JSON for use in the HTML GUI:
- From a local file:
  ```python
  python adhunt.html <ldif_results_directory>
  ```
- Download and execute in memory:
  ```python
  curl https://adhunt.netlify.app | python
  ```

### Browser
Run the HTML file in a browser to display and filter results:
1. Upload JSON files into ADHUNT.
2. Use the global filter to search for specific entries.
3. Query and display all Active Directory attributes.
4. Filter entities and save results as a .csv file.

For example, to find all managers:
- Filter for "Managers" and export the list as a .csv file.
- Useful for targeted tasks like sending phishing emails.

## Installation

- Using `curl`:
  ```bash
  curl https://adhunt.netlify.app > adhunt.html
  ```
- Using `wget`:
  ```bash
  wget https://adhunt.netlify.app
  ```
- From the browser:
  - Right-click -> Save As -> `adhunt.html`

ADHUNT requires no installation and can run completely in memory to dump domain information, then parse results locally in your browser at https://adhunt.netlify.app.

## Todo

- Python domain information collector
- BloodHound data converter
- Webhook encrypted extraction
