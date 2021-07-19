# CSS targeting for Links
A set of CSS rules that will set the default link styling in your email. 

## Intro
A lot of CSS 'resets' deal with stopping email clients default link styling of blue color and underlined. Although these are not really 'resets' as it is really just a way of over writing the current styles and all links will be styled differently based on designs. It is important to share how we can target email clients and adjust the color settings for links.

All of the CSS below will reset **ALL** links in an HTML document. So may not be the best solution if you want granular control of each link, which can be handled with class/id specifically or inline styles. Gmail App and Non-Gmail Accounts (GANGA) is the last email client still needing inline styles as the `<head>` is ignored.

## Code
*Generic reset*

The below meta tag sets the format detection to ignore, addresses, email, date and url - to hopefully ask the email client/browser to not adjust the format.

```
<meta name="format-detection" content="telephone=no,address=no,email=no,date=no,url=no">
```

The CSS below resets all links to `text-decoration: none;` and using the below we can ensure any anchor tags `<a>` inherit the color. We need to add `!important` so that outlook .com listens to the `color: inherit`. Outlook on Windows Desktop doesn't support `color:inherit;` so we need to set a specific color. 

```
a {
    color:inherit!important;
    color:#000;
    text-decoration: none;
    }
```

This is partially why this isn't necessarily a 'reset' as in browsers, all `<a>` have a default of blue and are underlined, in email the behaviour is the same, but styling links in email clients needs `!important` or specific CSS targeting. Having to set a specific color for Outlook Windows on Desktop obviously means styling then needs to happen inline. 

Also email clients auto-link telephone, dates, addresses, email addresses and urls - which need targeting below to over write email client styles.  

I've seen the below in a lot of emails so thought I should include it. To use it, the body will need `id="body"` - but I have not seen email clients not inheriting the other font styles. 

```
#body a {
    color: inherit;
    text-decoration: none;
    font-size: inherit;
    font-family: inherit;
    font-weight: inherit;
    line-height: inherit;
    }
```   

### Client specific

*Gmail* 

The below needs the `<body>` element to have the `class="body"` and the HTML needs to have a Doctype set, as Gmail turns the `<Doctype>` into a `<u>` tag.

```
u + .body a {
  color: inherit;
  text-decoration: none;
  font-size: inherit;
  font-weight: inherit;
  line-height: inherit;
  }
```

*Apple Mail / iOS*

```
a[x-apple-data-detectors] {
    color: inherit!important;
    text-decoration: none!important;
    font-size: inherit!important;
    font-family: inherit!important;
    font-weight: inherit!important;
    line-height: inherit!important;
    } 
```

```
[x-apple-data-detectors-type="calendar-event"] {
    color: inherit !important;
    -webkit-text-decoration-color: inherit !important;
    text-decoration: none !important;
    }
```

*Samsung Mail*

```
#MessageViewBody a {
    color: inherit;
    text-decoration: none;
    font-size: inherit;
    font-family: inherit;
    font-weight: inherit;
    line-height: inherit;
    }
```

*Outlook .com*

```
#root [x-apple-data-detectors=true],
a[x-apple-data-detectors=true]{
	color: inherit !important;
	text-decoration: inherit !important;
}
```

*Outlook Windows Desktop app*

```
<!--[if (mso)>
<style type="text/css">
a {
    text-decoration: none;
    }
</style>
<![endif]--> 
```
