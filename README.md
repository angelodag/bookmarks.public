bookmarks.public
================

This repository contains the single HTML file `index.html`.

The bookmarks file is a template which is designed to be edited by the user,
replacing the bookmarks in the single unordered-list with their own.

The bookmarks file contains some simple javascript which should allow simple
navigation and interactive use of the bookmarks, when opened via a browser.

It is also possible to add new bookmarks without opening the file in an editor.


Rationale
---------

I didn't like any of the online bookmark-syncing plugins/addins/tools I tested.

The idea of hosting an online bookmark server is appealing, but using the
power of Git it seems that having a local bookmark file should be pretty robust:

 * New items are added, generally one per line.
 * Existing items can be edited to add new tags.
 * Merges should be painless.

The included javascript magic is present solely to make the bookmarks manageable,
in my private copy I have 400+ bookmarks and with the tagging support present here
they will continue to work for me easily.


Using
-----

If you wish to use this bookmarks script, and are happy for your bookmarks
to be public, then just fork [this repository](https://github.com/angelodag/bookmarks.public) and you're done.

If you prefer to keep your bookmarks private, as I do, then you'll need to
clone the repository somewhere private.

I explain you how it is supposed to work:

In order to save new bookmarks, 
1. open the file in the browser
2. add the new bookmark (title, address and tags)
3. use the browser "save as" to save the modified page.

There is a big caveat, when you want to add a bookmark you do not have to di any other operation like filtering for tag, search or display the tags. 
If you save while the pages shows filtered data (generate by the internal javascript) then the page will contain the filtered data.
If you save while the tags are being shown, the tags will become part of the saved html.

There is another caveat, when you save the page, in the html you will get also the expanded reference to the page's current location, if you move it somewhere else then it will break unless you manually edit the page.

In general the html saved by the browser is rather ugly (long lines, lost alignment...) and this makes difficult to compare different versions of the file. For me , I use a "post-processing" script that keeps the alignment consistent across multiple save operations and removes the reference to the current location and file name (and some minor stuff, you can see it below):

```
#!/bin/bash
# 1 remove the expanded tags
# 2 break <a> on multiple lines
# 3 break <li> over multiple lines
# 4 remove empty lines
# 5 remove reference to file name and location
# 6 replace local reference to jquery with internet one
sed -i.bak -e 's/<a class="tagfilter".*<\/a>[,|.]//g' \
           -e 's/a>, <a/a>,\n <a/g' \
           -e 's/li><li/li>\n<li/g' \
           -e '/^\s*$/d' \
           -e 's/file:.*#/#/g' \
           -e 's/type="text\/javascript".*js"/type="text\/javascript" src="http:\/\/code\.jquery\.com\/jquery-2\.1\.1\.min\.js"/g' \
"$1"
```

Contributing
------------

If you wish to submit improvements to the javascript code, or layout, then I welcome forks & pull requests.

(If you submit a change feel free to add a link to your homepage/blog/whatever as part of that.  The sample bookmarks are only samples.)

Angelo (This page is mostly a copy of the one present in the original repository from [where I forked] (https://github.com/skx/bookmarks.public))
--
