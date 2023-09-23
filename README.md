# TotalCMS Arbitrary File Upload - XSS and steal cookies

## Author: (Sergio)

**Description:** TotalCMS is affected by Arbitrary File Upload - XSS vulnerability which allows Cross-Site Scriting (XSS) and also stealing session cookies

**Attack Vectors:** A vulnerability in "Total Depot" file upload sanitation allows you to upload a PDF / SVG /HTML file with hidden alert Cross-Site scripting (XSS) and steal the user cookies.

---

### POC XSS PDF/SVG/HTML:


When logging into the admin panel (https://www.totalcms.co/demo/total-cms/admin/), we will go to the "Total Depot" off the Administration Site and we upload the PDF file with the hidden XSS and we see that we can execute it and the XSS appears.


![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/59567372-3336-4efd-aa24-2293ee2018c3)


![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/1f2050a8-008c-4002-aeda-8ec4ecb3a406)




</br>

### Additional Information:
[http://www.cmsmadesimple.org/](https://www.totalcms.co/)

https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html
