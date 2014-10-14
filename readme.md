# Intro

Over the weekend, I came across [pigshell](http://pigshell.com/v/0.6.2/), a webapp that is supposed to let
you "unix the web." Leaving aside the fact that the Web is
[fairly well Unix'd](http://en.wikipedia.org/wiki/Usage_share_of_operating_systems#Servers_on_the_Internet), pigshell is sort of neat... you can browse Internet resources -- web pages, your Facebook and your Dropbox -- from a shell-style interface, do a li'l
data munging, and throw up some slick visualizations from what you've found. It's well done, and a cool experience.

THat said, the ability to send a Facebook post from a command isn't about to disrupt my slack-jawed, drooling point-and-click 
Internet experience.
And I'm really not so hot on having to run a small server on my desktop to access local files, or the reduplication
of standard Unix utilities with some nonstandard interfaces. 
And I would love to avoid web app crud. I don't know what a cross-origin browser request is or why I can't make one, and please just don't tell me. Pigshell does some cool wizardry to get out of the sandbox, but I would rather just not be playing in sandbox because I am an adult.

That ability to grab data from the web, do some light processing, and
kick out a visualization was pretty cool. If I could do that from the best shell, *my* shell, that shell that already exists on my computer, then we're talking. Especially if it could integrate with tools that I'm already using and I will continue using until you pry them out
of my cold, dead hands, like awk and Gnuplot. More specifically, if I had a small library of D3 templates that I could kick data to using
a tiny shell command, I think that would bring my data analysis closer to my actual data in a really helpful way. Pigshell's templates
are an awesome starting place (which I will shamelessly copy). 

To that end, I've started writing a tiny suite of tools (right now, very rough scripts) that would allow me to do what pigshell can do, from the 
comfort of my own $HOME. I'm too lazy to deal with a whole new way of doing things. Keep it Simple, Stupid.
So I've got a couple very, very rough tools:

- [table2js](bin/table2js) is a Python script that takes in HTML document and a CSS selector, and spits out an array of arrays of the text inside what's selected (some examples will make clear what I mean by this). With extra arguments it will build up an array of JSON objects, rather than an array of arrays.
The program name and the interface are cribbed from the pigshell command of the same name.
It depends on lxml and cssselect.

- [newplot](bin/newplot) will throw up some JSON into a D3 template and open it up. Whew! Right now it requires Chrome, but one could very easily edit it to use a different browser. Guess where I came up with the clever name.

# Example

Again, compare to pigshell's [examples](http://pigshell.com/v/0.6.2/doc/README.html) and note how I copied them.

```bash
curl http://pigshell.com/sample/life-expectancy.html | table2js -e "table.wikitable tr" foo country data | newplot templates/d3-worldmap1.html
```

Oh no, no Facebook integration, what a shame. Not to be snarky but I got your Dropbox:

```bash
ls ~/Dropbox
```
