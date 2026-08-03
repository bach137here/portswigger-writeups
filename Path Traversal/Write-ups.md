
This part isn't too much learning stuffs, cases; so I'll gather all write-ups and notes into this only file.

- **Case 1**
https://insecure-website.com/ ==loadImage?filename=../../../etc/passwd==

- **Case 2** Using absolute path
https://insecure-website.com/ ==loadImage?filename=/etc/passwd==

- **Case 3** Deal with ```
$filename = str_replace('../', '', $filename);

 use 