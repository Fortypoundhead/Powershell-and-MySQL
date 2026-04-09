# Powershell Link Scraper with MySQL Storage

This repository contains a PowerShell script (`lex.ps1`) that demonstrates how to fetch links from a website and store the link text and URL in a MySQL database.

## What it does

- Loads the MySQL .NET Connector
- Opens a connection to a MySQL server
- Downloads a web page from a seed URL
- Extracts all HTML links from the page
- Inserts each link's anchor text and URL into a MySQL table

## Prerequisites

- PowerShell 5.1 or later
- MySQL server accessible from the machine running the script
- MySQL .NET Connector installed
- A MySQL database and user configured

## Configuration

In `lex.ps1` you should update the following values as needed:

- `$SeedURL` – the initial website URL to crawl
- MySQL connector path:
  - `Add-Type -Path 'C:\Program Files (x86)\MySQL\Connector NET 8.0\Assemblies\v4.5.2\MySql.Data.dll'`
- Connection string:
  - `server=127.0.0.1;uid=lex;pwd=lex;database=lex`

## Database table

The script writes into a table named `main` and expects at least these columns:

- `anchortext` (text or varchar)
- `url` (text or varchar)

Example table definition:

```sql
CREATE TABLE main (
  id INT AUTO_INCREMENT PRIMARY KEY,
  anchortext TEXT,
  url TEXT
);
```

## Usage

Run the script from PowerShell:

```powershell
.\lex.ps1
```

## Notes

- The script currently inserts raw values directly into SQL statements. In production, parameterized queries should be used to avoid SQL injection and handle special characters.
- The script only crawls the seed page once and does not follow links recursively.
- If the MySQL connector or the connection details are incorrect, the script will fail when opening the database connection.

## Customization

You can adapt the script to:

- parse multiple pages
- use parameterized inserts
- store additional data such as the page title or HTTP status
- filter links by domain or file type

## License

This repository is provided as a simple example/demo without warranty.