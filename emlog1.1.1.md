**File upload vulnerability exists in emlog. Procedure**

official website：https://www.emlog.net/

Buggy version：1.1.1

1. First, find the function point with the vulnerability. The backup file uploaded here will be directly executed and the sql commands can be controlled

![WPS图片(1)](https://user-images.githubusercontent.com/131507436/233838508-1cd7cb29-2374-44a8-8b51-ed5c7cdecf40.png)

Find the function point source code through the route

![WPS图片(2)](https://user-images.githubusercontent.com/131507436/233838514-aedd9f91-f8f9-4dfd-86dc-d36208877eee.png)

![WPS图片(3)](https://user-images.githubusercontent.com/131507436/233838516-f7b870da-993e-428b-ae4b-4bc44fa80c95.png)

2. The whole if condition above restricts the size and suffix of the uploaded file, but does not restrict the content of the sql file. Therefore, you only need to import the specified sql file to cause SQL injection.

checkSqlFileInfo() Checks whether the file is a normal file and the specified file format.

![WPS图片(4)](https://user-images.githubusercontent.com/131507436/233838519-5f2e1924-40b6-46ff-b51b-4f3bbff61827.png)

![WPS图片(5)](https://user-images.githubusercontent.com/131507436/233838521-ad044369-7b07-4518-b40d-2a4112881bda.png)

3.Bakindata() executes the sql file directly

Save the contents of the sql file as an array, then iterate through the contents of the array and execute the SQL statement using query().

![WPS图片(6)](https://user-images.githubusercontent.com/131507436/233838525-15608bf5-617d-4c71-9beb-0ee01580be1a.png)

![WPS图片(7)](https://user-images.githubusercontent.com/131507436/233838530-c6816dc7-3571-4aed-8f07-0bc4307bf935.png)

4.Bakindata() executes the sql file directly

Save the contents of the sql file as an array, then iterate through the contents of the array and execute the SQL statement using query().

![WPS图片(8)](https://user-images.githubusercontent.com/131507436/233838533-d5d711e0-ff41-4b28-a6c9-e482bd089674.png)

Write a sentence to a log file using MYSQL log writer

![WPS图片(9)](https://user-images.githubusercontent.com/131507436/233838538-71baa8cc-b1f9-4172-a68d-7f465a89f341.png)
