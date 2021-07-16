# email-css-resets
A repository to hold all CSS resets/normalisation from past and present email clients.

The aim of these CSS files is to record CSS in use by email developers to normalise the behaviour of HTML elements across email clients. 

There are two types of CSS -

## 1. General CSS normalisation
CSS that will affect change needed across email clients to normalise behaviour. 

For example: 
```
table { border-collapse: collapse; }
```

With all emails currently needing to include the table HTML element, even if only for Outlook, the overall normalisation to collapse table borders will stop gaps appearing between tables and cells. 

## 2. Email client specific CSS
CSS that will reset/override specific styles an email client will force on HTML elements. 

For example:
```
body[data-outlook-cycle] a {
  color: inherit !important;
  text-decoration: none !important;
}
```

The above CSS targets the Outlook apps on Android and iOS devices which change links to blue and add an underline, without the email developer adding those attributes. This CSS 'reset' sets the color to inherit from the parent element and not to have an underline.


Two main files - 

<a href="https://github.com/JayOram/email-css-resets/blob/main/old-CSS-resets.css"> Old CSS resets</a><br>
<a href="https://github.com/JayOram/email-css-resets/blob/main/CSS-normalise.css"> Current CSS resets/normalisation</a>

I would love anyone to send updates / pull requests with any CSS resets they find in old templates or know of? 

Thanks to <a href="https://github.com/TedGoas">Ted Goas</a> for updating the read me to look much better!

Contributors:
<a href="https://github.com/M-J-Robbins">Mark Robbins</a>, <a href="https://github.com/hteumeuleu">Rémi Parmentier</a> and hat tip to <a href="https://github.com/cossssmin">Cosmin Popovici</a> who has created <a href="https://github.com/maizzle/email-normalize">email-normalize</a> an npm package to use email normalise and reset CSS in builds. 
