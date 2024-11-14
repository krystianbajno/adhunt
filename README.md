# ADHUNT
[![CodeFactor](https://www.codefactor.io/repository/github/krystianbajno/adhunt/badge)](https://www.codefactor.io/repository/github/krystianbajno/adhunt)
[![Codacy Badge](https://app.codacy.com/project/badge/Grade/557adc031264478bb9ee8f2227a3c3a6)](https://app.codacy.com/gh/krystianbajno/adhunt/dashboard?utm_source=gh&utm_medium=referral&utm_content=&utm_campaign=Badge_grade)

**ADHUNT** is a versatile polyglot file (Bash, PowerShell, Python, HTML) for overviewing domain information. It operates seamlessly across different environments without the need for installation. You can either save it directly from the website or execute it in-memory.

### Collectors:
- **Python**: `ldap3` (todo)
- **PowerShell**: `New-Object DirectoryServices.DirectorySearcher`
- **Bash**: `ldapsearch`

### Converters:
- **Python**: Converts `ldapsearch` LDIF results into ADHUNT JSON.
- **Python**: Converts BloodHound JSON into ADHUNT JSON. (todo)

### GUI:

- **HTML**: Runs directly in your browser as a static website and is not communicating with hosting HTTP server. You can run it locally or remotely.

## Usage Scenarios:

### PowerShell
**Run the HTML file as a PowerShell script to dump domain information (users, groups, computers, and group policies):**
- From a local file:
  ```powershell
  iex(gc -path adhunt.html -raw)
  ```
- Download and execute in memory:
  ```powershell
  iwr https://adhunt.netlify.app | iex
  ```

### Bash
**Run the HTML file as a Bash script to dump domain information (requires `ldapsearch`):**
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
**Dump domain into LDIF using python collector:**
- From a local file:
  ```python
  python adhunt.html <ldif_results_directory> --dump
  ```
- Download and execute in memory:
  ```python
  curl https://adhunt.netlify.app | python
  ```
  
**Parse LDIF results into JSON for use in the HTML GUI:**
- From a local file:
  ```python
  python adhunt.html <ldif_results_directory>
  ```
- Download and execute in memory:
  ```python
  curl https://adhunt.netlify.app | python
  ```

**Convert BloodHound results into ADHUNT JSON format:**
- From a local file:
  ```python
  python adhunt.html <bloodhound_results_directory> --bloodhound
  ```
  
- Download and execute in memory:
  ```python
  curl https://adhunt.netlify.app | python
  ```

**In order to convert ADHUNT LDIF results into BloodHound, use:**
- https://github.com/SySS-Research/ldif2bloodhound
- https://github.com/gquere/bloodhound_linux

### Browser
**Run the HTML file in a browser to display and filter results:**
1. Upload JSON files into ADHUNT.
2. Use the global filter to search for specific entries.
3. Query and display all Active Directory attributes.
4. Filter entities and save results as a .csv file.

### Examples
To find all managers:
- Filter for "Managers" - you will get all manager related entries.
- You can export the seperate lists as .csv files, it is useful when searching for emails.

To find the groups the user belongs to:
- Upload users.json and groups.json.
- Filter for username in the filter input
- You will get the user, his groups are in `memberOf`.
- You will get all groups the member belongs to in `member` attribute of found groups.

To find all users who's name is "Mike" AND account is enabled:
- Filter for `Mike 512 enabled`

To find all users who's name is "Mike" AND account is disabled:
- Filter for `Mike 514 disabled`

To find account who's name is Mike Smith:
- Enter `Mike Smith` in filter.

To find account who's name is Mike Smith AND is an administrator:
- Enter `Mike admin` in filter.
- Enter `Mike Smith admin` in filter.

To find domain admin:
- Filter for `domain admin`.
- You will get all Domain Administrators in Users.

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
