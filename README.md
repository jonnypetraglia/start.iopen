# start.iopen #

start.iopen is an open-source clone of [start.io](http://start.io), a startpage
for your favorite links.

It's designed to be **open-source** and therefore **self-hostable**, work
**locally*, and be so simply written in **vanilla JS** that it should run in
all modern browsers, and -most importantly- be essentially self-contained in
**one HTML file** and your sites in **one JSON file**. And lastly: it's designed
to load even when **despite internet failure**.


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

As stated, start.iopen is self-contained in one file. But there's also external
skins that are *entirely optional*. A theme is just two files inside the
'themes' directory:

  (1) <theme-name>.css
  (2) <theme-name>.templ

start.iopen uses [John Resig's Micro-Templating](http://ejohn.org/blog/javascript-micro-templating/)
for templating so it's fast and simple.

## Ideal usage ##

The setup to start.iopen involves just hosting your JSON file somewhere. That's
it.

From there you can either host index.html (+themes if desired) or store them
locally on your machine which will allow you to access your sites even when the
internet is down. This is possible because start.iopen caches your sites using
HTML localStorage so even if the internet is down, the page will load.

Why load your list of favorites if the internet is down? Because it's the era of
the web, of HTML5, of life within the browser and favorites are not just
websites anymore.
(Example: [FireSSH](https://addons.mozilla.org/EN-us/firefox/addon/firessh/))

Also network problems are annoying enough without seeing a loading icon every
time you open a new tab.


## Local usage ##

Using start.iopen locally is indeed possible, with some caveats depending on
the browser you use. Because browser security is ever tightening, some browsers
are more strict for local files.

For example, Chrome will not let a local file interact with any other local
files via AJAX, which is how start.iopen fetches the JSON.

Meanwhile, Firefox works flawlessly because they let files access other files
in the same local directory.


### JSON ###

Thus there are two solutions:

  #### 1. Find a browser-specific workaround

  For Chrome, it would be launching it with the parameter
  `--allow-file-access-from-files`, which admittedly does lessen security overall.

  #### 2. Make the JSON "JSON-esque"

  Adding the line:
    ```jsonData=```
  to your sites JSON file will then let start.iopen read it as though it were JS,
  making browsers like Chrome happy.

### Themes ###

For themes, the only real solution is to paste the contents of the theme(s) you
want into `index.html` inside a `<script>` tag like so:

```
<script type="text/html" id="startiopen_templ_{{THEME_NAME}}">
  ... file contents ...
</script
```

There are already two templates for "Default" and "Mobile" that work along this
practice.


### Writing your own theme ###

You can easily write your own theme. You can write an HTML template using your
JSON data as the variable `groups`, then just write whatever CSS you want to
style it. You can include any valid HTML inside your template, including
Javascript, so you can do things like `document.title = 'mah title';`.

Here are a few tips about writing your own theme:

  - Assign the id of the div with the 'group' class to the group name; this will
    allow you to view just that group and even link to just it.
    (```<div class="group" id="<%=groupName%>">```)
  - Avoid using hardcoded ids. Mostly just so it won't interfere with the above.
  - Make sure your styles stay contained inside `<main>`, otherwise things like
    the menu and preferences will look weird.


And lastly, if you write a theme that you like, feel free to submit it to the
[Github repo](http://github.com/notbryant/start.iopen) or create a
[Gist](https://gist.github.com/) for it or just email me (address is in the
commit log).


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
