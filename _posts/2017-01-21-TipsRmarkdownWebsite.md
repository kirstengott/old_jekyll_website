---
title: "5 Tips for Making an Rmarkdown Website with Rstudio"
crosspost_to_medium: true
---

TL;DR:


1. Make all code chunks have different names


2. Clean the cache before rebuilding the website


3. Make the _site.yml simple, adding details to individual pages


4. Use the '.gitignore' file and the 'exclude:[]' option in the _site.yml


5. Include a 'footer.html', 'header.html', and 'styles.css' in the _site.yml file



In picking a tool for creating a website to display a some biological data analysis for the [ctenophore](https://mnemiopsis.github.io/) project, I looked for tools that would seemlesly fit into my current data analysis framework (primarily R coding in Rmarkdown using Rstudio as my text editor). The obvious choice was an Rmarkdown website. 

The procedure was simple: just copy all of my .Rmd files into a directory, create an _site.yml file, fire up an 'Rstudio Project' and click the 'Build' button in Rstudio. Yes it was that easy! 

However, I did run into a couple of hiccups during this process which led me to make this post documenting things I initially did wrong/poorly and improved upon for my finished product. At the end of this post I'll put a version of the _site.yml that I will use if I ever do this sort of project again.


### 1. Make ALL code chunks have unique names 

I ran into this issue because I have a parameterized report that I use for the majority of my basic RNA-seq analysis. I copied several different versions of this report into my website directory, not bothering to change the names of the named code chunks. I figured that during the build process the Rmarkdown renderer would either error out, or make them unique on the fly. 

Neither of those events occured. In fact, the build went to completion. However, when I looked at my website all of the parameterized reports I had used were multiple copies of the same report! I tried a few different methods to remedy the problem, none that worked consistently (involving knitr caching). Then I realized that all of the reports get evaluated in the SAME build. This led me to adding a unique identifier to the code chunks that I had repetitive names for within my parameterized reports.

Note that this is only a problem if you name your code chunks and use the same sort of parameterized report in your build, unnamed code chunks will be given numbers sequentially.

### 2. Clean the cache before rebuilding the website

A lot of my pages took a lot of time to render, so I started caching parts of them to speed up the rendering while I was trouble-shooting different aspects of the website layout. However, I would sometimes make changes to plots that wouldn't show up because old code chunks would be cached and used in the final document rather than re-rendering any chunks that had been modified within code chunk.


### 3. Make the 'output' portion of _site.yml simple, adding details to individual pages

I usually like to have a table of contents on most of my R markdown documents, but for this website it wasn't necessary for the whole thing. I ended up adding a table of contents to several of the pages, as well as bibliographies to a couple within the individual pages themselves rather than configuring it in my _site.yml.


### 4. Use the '.gitignore' file and the 'exclude:[]' option in the _site.yml

Some of the data that I was working with on this project took up a lot of space making them not very 'git' friendly. Make sure to exclude those files when you are building you website or else when you try to build your R studio instance may die! Also, add them to your .gitignore or face git death!


### 5. Include a 'footer.html', 'header.html', and 'styles.css' in the _site.yml file

These are built into the R markdown YAML header syntax with the 'includes' section and make it easy to fix little issues with CSS, as well as adding headers and footers. Yay for easy ways to integrate a little HTML into my markdown world!



And of course a sample _site.yml:

<script src="https://gist.github.com/kirstengott/1389e0422e5e9fe168ae7c0abe03fefd.js"></script>
