---
project: File-Smuggling
stars: 387
description: HTML smuggling is not an evil, it can be useful
url: https://github.com/eddiechu/File-Smuggling
---

HTML smuggling is not an evil, it can be useful
===============================================

### File Smuggling Builder

This is a self-contained HTML app, handy, supports Windows, Mac, Linux and mobile.

It adopts HTML smuggling technique, leverages HTML5 and JavaScript to embed encoded file into HTML file, when user runs the JavaScript code in browser, it decodes the embedded payload, which, in turn, assembles the target file on the destination device.

You can convert your file to HTML encoded format, with password protected, then use it as email attachment or file download from web.

Download filesmugglingbuilder.html from this repository or try it online

https://eddiechu.github.io/filesmugglingbuilder.html

### Example

###### 1a. Choose target file `putty.exe`, then generate `putty.exe.html`

###### 1b. Open `putty.exe.html`, then retrieve `putty.exe`

###### Download putty.exe.html from this repository or try it online

https://eddiechu.github.io/putty.html (password is password)

###### 2a. Choose target file `Sample Document.docx`, then generate `Sample Document.docx.html`

###### 2b. Open `Sample Document.docx.html`, then retrieve `Sample Document.docx`

###### Download Sample Document.docx.html from this repository or try it online

https://eddiechu.github.io/sampledocx.html (password is password)

### HTML Smuggling Tachnique

###### Use of JavaScript Blob

When working with Javascript, the file can be created by using a Javascript Blob. A Blob is a representation of payload.

```
  var bobject = new Blob([payload], {type: 'octet/stream'});
```

###### Using the URL.createObjectURL

It invoking the click action from within the Javascript, we mimic the user clicking on the link and starting the file download

```
  var hiddenobject = document.createElement('a');
  var url = window.URL.createObjectURL(bobject);
  hiddenobject.href = url;
  hiddenobject.download = targetfilename;
  hiddenobject.click();
```

Due to encoded patterns, no original file content passes through the network, bypassing email scanners, proxies and sandboxes.

As security admin, if you don't want user to bypass, you may fine tune the dection rule based on it's characteristics or simply block HTML file.

Reference

https://attack.mitre.org/techniques/T1027/006/

#html smuggling #payload #javascript #pentest #poc #html #smuggling #tool
