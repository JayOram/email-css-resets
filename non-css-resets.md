# Non-CSS resets / normalise
HTML code to normalise and reset email client behaviour.

## Intro
After many discussions with other emailgeeks I realised there wasn't a place that had some of the other normalise or reset elements that don't fall into the CSS of an email.

Keep in mind that these may not be applicable to all emails, so use only where needed.

## Code

*Set the viewport*

The below meta tag helps set up the viewport for your email. 

`width=device-width` sets the width of th viewport to the width of the device.

`initial-scale=1` sets the initial 'zoom' value of the screen to 1 or 100%

```<meta name="viewport" content="width=device-width, initial-scale=1" />```
   

The below meta tag sets the format detection to ignore, addresses, email, date and url - to hopefully ask the email client/browser to not adjust the format.

```
<meta name="format-detection" content="telephone=no,address=no,email=no,date=no,url=no">
```


The below meta tag is used to disable apple mail reformatting HTML code

```
<meta name="x-apple-disable-message-reformatting" />
```


The next fix is for a number of Micorsoft Outlook specific anomalies and some other email client fixes - this is placed inside the body of the email:

```
<span style="display: none;"><!-- [if mso]>
<xml>
<o:OfficeDocumentSettings>
<o:PixelsPerInch>96</o:PixelsPerInch>
</o:OfficeDocumentSettings>
<w:WordDocument>
<w:DontUseAdvancedTypographyReadingMail/>
</w:WordDocument>
</xml>
<! [endif]--></span>
```


Wait - shouldn't this be in the `<head>` of the email? The issue we are seeing is that Gmail App Non Gmail Account (GANGA) 96 is being printed, even if it is in the head. Therefore moving it to the `<body>` allows us to use `<span style="display: none;">...</span>` to hide the 96 from all other email clients except Microsoft Outlook.


Next the mso-comments -  `<!-- [if mso]>...<! [endif]-->` which includes a space to keep the mso comments from showing in T-online.de - more details on this blog [MSO Comments](https://lessonsinemail.com/articles/mso-comments#t-online).


The below section is a fix for Outlook 120 dpi when using VML. You should check out this amazing article from Courtney Fantinato on [Correcting Outlook DPI Scaling Issues](https://www.courtneyfantinato.com/correcting-outlook-dpi-scaling-issues/).
 
```
<o:OfficeDocumentSettings>
<o:PixelsPerInch>96</o:PixelsPerInch>
</o:OfficeDocumentSettings>
```


The next section stops Outlook changing the text. Shout out to Nicole Merlin and this article [Microsoft introduces controversial new “Advanced Typography” features for Outlook Classic](https://knak.com/blog/microsoft-introduces-advanced-typography/):
* Changing left-aligned text to be fully justified
* Adding hyphenation to words
* Adjusting spacing between words
* Adjusting spacing between letters

```
<w:WordDocument>
<w:DontUseAdvancedTypographyReadingMail/>
</w:WordDocument>
```
