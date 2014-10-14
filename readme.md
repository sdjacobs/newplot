# Intro

Inspired by [pigshell](http://pigshell.com/), I'm writing a couple of tiny scripts to do some light web scraping
and push data to D3 templates.

- [table2js](bin/table2js) is a Python script that takes in HTML document and a CSS selector, and spits out an array of arrays of the text inside what's selected (some examples will make clear what I mean by this). With extra arguments it will build up an array of JSON objects, rather than an array of arrays.
The program name and the interface are cribbed from the pigshell command of the same name.
It depends on lxml and cssselect.

- [newplot](bin/newplot) will throw up some JSON into a D3 template and open it up. Whew! Right now it requires Chrome, but one could very easily edit it to use a different browser. Guess where I came up with the clever name.

# Example

Compare to pigshell's [examples](http://pigshell.com/v/0.6.2/doc/README.html) and note how I copied them.

```bash
curl http://pigshell.com/sample/life-expectancy.html | table2js -e "table.wikitable tr" foo country data | newplot templates/d3-worldmap1.html
```

Oh no, no Facebook integration, what a shame. Not to be snarky but I got Dropbox:

```bash
ls ~/Dropbox
```
