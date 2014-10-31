# Intro

Inspired by [pigshell](http://pigshell.com/), I'm writing a couple of tiny scripts to do some light web scraping
and push data to D3 templates.

- [tadge](bin/tadge) is a Python script that takes in HTML document and a CSS selector, or a text file, and spits out an array of arrays of the text inside what's selected (some examples will make clear what I mean by this).
With extra arguments it will build up an array of JSON objects, rather than an array of arrays.
The program was originally called "table2js", with the name and the interface cribbed from the pigshell command of the same name. 
But I found that I needed options for comma- and whitespace-delimited input and output, and some other helpful options.
It stands for TAble nuDGE. 
It depends on lxml and cssselect.

- [newplot](bin/newplot) will throw up some JSON into a D3 template and open it up.
Right now it requires Chrome, but one could very easily edit it to use a different browser.
Guess where I came up with the clever name.

# Example

Compare to pigshell's [examples](http://pigshell.com/v/0.6.2/doc/README.html) and note how I copied them.

```bash
curl http://pigshell.com/sample/life-expectancy.html | tadge -e "table.wikitable tr" foo country data | newplot d3-worldmap1.html
```

Oh no, no Facebook integration, what a shame. But my shell does have Dropbox integration:

```bash
ls ~/Dropbox
```

Contra pigshell, my system integrates with tools I already use. Nothing will ever beat Gnuplot for easy plotting of X-Y data.

```bash
curl http://en.wikipedia.org/wiki/World_population_estimates | tadge -e "table.wikitable tr" -fs -n 0,3 -c' ' |  gnuplot -e "plot '-'
```

Line graphs are fun!

```bash
curl http://en.wikipedia.org/wiki/World_population_estimates | tadge -e "table.wikitable tr" -fs -n 0,3 | newplot d3-linegraph.html
```

Right now, I'm dealing with a database full of book records from a library. What's in it?

```
sqlite3 books.sql 'select language,count(*) from books group by language' | tadge -i'|' name value | newplot d3-pie.html
```
