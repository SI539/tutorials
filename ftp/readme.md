# FTP Client Setup Tutorial

## Cyberduck
### Step 1. Click "Open Connection"
![Open Connection](./pics/open_connection.png)

---

### Step 2. Choose SFTP
![Choose SFTP](./pics/choose_sftp.png)

---

### Step 3. Setup SFTP server information
1. In the server field, enter sftp.itd.umich.edu
2. Port number is 22
3. In the username field, enter your uniqname
4. In the password field, enter your kerberos password
5. Click connect

![Setup Server Information](./pics/setup_server_connection.png)

---

### Step 4. If you correctly connected, you can see your file structure on the ftp server
Now you can drag and drop files to that window to upload your files, or double click files to download.
![FTP View](./pics/ftpview.png)

---

### [Optional] Step 5. Add the ftp server to bookmark for quick access
1. Click the bookmark icon
![Bookmark Icon](./pics/bookmarkicon.png)
2. Everything should be filled correctly, if not just manually enter those fields
![Bookmark Edit](./pics/bookmark_edit.png)
3. Close the window, and now the site is stored in your bookmark
![Bookmark View](./pics/bookmark_ready.png)

### Step 6. Upload your webpage to the server
Let's take week1's discussion assignment for example  
1. I have file structure like this. I put the index.html file under the `dis1` folder and I put the picture inside the `dis1/pic/` folder.
![HTML files](./pics/html_files.png)
2. In Cyberduck, go to `Public/html`, there should be a default index.html created by UM ITS
![Cyberduck Public](./pics/cyberduck_html.png)
3. Drag your `ds1` folder on your computer to the `Public/html` folder on the server
![File Upload](./pics/file_upload.png)
4. Open your browser an type the URL `http://www-personal.umich.edu/~youruniqname/dis1` and you can see your webpage online
![Webpage](./pics/webpage.png)
