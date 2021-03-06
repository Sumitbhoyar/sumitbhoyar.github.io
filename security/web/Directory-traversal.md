
# Directory traversal

Directory traversal vulnerabilities allow attackers to access arbitrary files on your system. They tend to occur in older technology stacks, which map URLs too literally to directories on disk.

**Risk**

- File system could be compromised.

**Protection**

Following search on Google could be used to identify if your site is vulnerable- `site:<yourdomain.com> inurl:file=`

- Use a Content Management System

A modern CMS will protect against directory traversal.

- Use Indirection

Each time a file is uploaded, construct a “friendly” name for this on your site, and when the file is accessed, perform a lookup in your data-store to discover the actual file path

- Segregate Your Documents

Hosting documents on a separate file-server or file partition, or in cloud storage, is a good idea too. This will allow you to prevent mixing public documents and more sensitive material.

- Sanitize Filename Parameters

Restrict use of file path like ../, ~/ etc

- Run with Restricted Permissions

Make sure the server process can only access the directories it needs.