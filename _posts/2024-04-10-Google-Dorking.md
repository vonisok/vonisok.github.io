---
title: "Google Dorks"
date: 2024-04-10 12:00:00 -500
categories: [OSINT]
tags: [recon]
---
# Google Dorks

Google Dorks are search queries that use advanced search operators in Google to find specific information that is not readily available on a website. They can be used to discover vulnerable web resources by searching for specific file types, error messages, administration panels, and sensitive files. Here are some examples of Google Dorks that can help find potentially vulnerable web resources:

### Sensitive Directories


`intitle:"index of" "/admin/"`

 Finds web server directories that contain administrative functions.

`intitle:"index of" backup`

 Finds directories named "backup".

### Configuration Files Exposed
```code
filetype:env "DB_PASSWORD"
```
Finds environment files that may expose database passwords.

```code
filetype:conf inurl:web.config inurl:ftp
```

Finds web server configurations that include FTP credentials.

### Database Files Exposed

```code
filetype:sql intext:"INSERT INTO" (password|username)
```

Finds SQL dump files containing passwords or usernames.

```code
filetype:sql site:com inurl:wp-content/backup-db
```

Finds WordPress database backups.

### Error Messages Revealing Software Vulnerabilities
```code
"PHP Parse error" | "PHP Warning" | "PHP Error"
```
Finds pages with PHP error messages.

```code
intext:"sql syntax near" | intext:"syntax error has occurred" filetype:sql
```

Finds SQL syntax error messages that may reveal vulnerabilities.

# Sensitive Documents Exposed
```code
intitle:"index of" "parent directory" intext:"[confidential]" (doc|pdf)
```

Finds directories containing files marked as confidential in either DOC or PDF format.

```code
filetype:pdf "confidential" not "for distribution"
```

Finds PDF documents marked confidential.

# Admin Login Pages
inurl:admin inurl:login: Finds admin login pages.
intitle:"login page" intext:"admin": Finds administrative login pages by title and text.

# Publicly Exposed Documents and Spreadsheets
filetype:xls | filetype:xlsx intext:email | intext:phone: Finds Excel files containing email addresses or phone numbers.
filetype:doc | filetype:docx intext:confidential: Finds Word documents containing the word "confidential".