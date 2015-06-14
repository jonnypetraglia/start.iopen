# start.iopen #

start.iopen is an open-source clone of [start.io](http://start.io), a startpage
for your favorite links.

It's designed to be **open-source** and therefore **self-hostable**, work
**locally*, and be so simply written in **vanilla JS** that it should run in
all modern browsers, and -most importantly- be essentially self-contained in
**one HTML file** and your sites in **one JSON file**.


## Editing your sites ##

Your sites are stored in a JSON file with the following format:

```
{
  "Group 1": {
    "Site A": "http://sitea.com",
    "Site B": "http://siteb.com",
  },
  "Group 2": {
    "Site Manfred": "http://planmanfred.com"
  }
}
```

That simple.


## Themes & "One File" ##

Themes are stored separately but are entirely optional and are made of two parts

  (1) <theme-name>.css
  (2) <theme-name>.templ

start.iopen uses [John Resig's Micro-Templating](http://ejohn.org/blog/javascript-micro-templating/)
for templating.

You can easily write your own theme by using your JSON data which is available
via the `groups` variable, write your own CSS, and add the name of your theme to
 the `themes` variable in the first `script` tag in `body`.


## Using Locally ##

Using start.iopen locally is indeed possible, with some caveats depending on
the browser you use. Because browser security is ever tightening, some browsers
are more strict for local files.

For example, Chrome will not let a local file interact with any other local
files via AJAX, which is how 

For example, Firefox works flawlessly because they let files access other files
in the same lcoal directory.


### JSON ###

Thus there are two solutions:

#### 1. Find a browser-specific workaround

For Chrome, it would be launching it with the parameter
`--allow-file-access-from-files`, which admittedly does lessen security overall.

#### 2. Make the JSON "JSON-esque"

Adding the line:
```jsonData=```
to your sites JSON file will then let start.iopen read it as though it were JS,
making Chrome Happy.

### Themes ###

For themes, the only real solution is to paste the contents of the theme(s) you
want into `index.html` inside a `<script>` tag like so:

```
<script type="text/html" id="THEME_NAME">
  ... file contents ...
</script
```

There are already two templates for "Default" and "Mobile" that work along this
practice.

 

## Things lacking from start.io ##

start.iopen does not have feature parity with start.io nor does it intend to.

  - Colors: currently this is omitted to make the JSON more concise, but I plan
    to implement it soon.
  - Stats: things like "click/lastClicked/lastUpdated"; but really the goal is
    to create a quick, fast starting page, not an avenue to datamine onesself.
  - Updates: checking if a site has "updated" is better reserved to feed readers
    and utilities that can handle sites that require authentication (i.e. gmail).
  - Site Management: no more fancy GUI, "Trash", etc; a JSON file should be enough
  - Bookmarklet: no "quick adds" to the JSON file
  - Antiquated iPhone interface: just......yeah
  - Requires JS: though the modern web is created with JS so really NBD
