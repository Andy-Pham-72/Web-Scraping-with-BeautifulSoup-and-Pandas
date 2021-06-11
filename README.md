# Web Scraping with Beautiful Soup and Pandas



Web scraping is the process of using bots to extract content and data from a website.

Unlike screen scraping, which only copies pixels displayed onscreen, web scraping extracts underlying HTML code and, with it, data stored in a database. The scraper can then replicate entire website content elsewhere.

Web scraping is used in a variety of digital businesses that rely on data harvesting. Legitimate use cases include:

- Search engine bots crawling a site, analyzing its content and then ranking it.
- Price comparison sites deploying bots to auto-fetch prices and product descriptions for allied seller websites.
- Market research companies using scrapers to pull data from forums and social media (e.g., for sentiment analysis).

## Table of Contents
[1. Making Database From Scratch With Beautiful Soup](#I.-Making-Database-From-Scratch-With-Beautiful-Soup) <br>
- [Scrape The Data](#Scrape-The-Data) 
- [Make A Database](#Make-A-Database)

[2. Web Scraping Using Pandas](#II.-Web-Scraping-Using-Pandas) <br>
- [Get The URL](#Get-The-URL) 
- [Read The HTML Webpage Into Pandas](#Read-The-HTML-Webpage-Into-Pandas)
- [Data Cleaning](#Data-Cleaning) 
- [Quick Exploratory Data Analysis](#Quick-Exploratory-Data-Analysis)<br>


## I. Making Database From Scratch With Beautiful Soup

There are a number of different packages available for web scraping, and one of the most popular is [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/). Beautiful Soup parses web content into a Python object and makes the [DOM](https://en.wikipedia.org/wiki/Document_Object_Model) queryable element by element. Used in conjunction with a requests package, it makes web scraping very easy!

---
### Installation of Beautiful Soup (if haven't done so)
In the `bash` terminal or `Anaconda Prompt`,run:
```bash
conda install beautifulsoup4
```
---


```python
# Standard imports
import pandas as pd

# For web scraping
import requests
import urllib.request
from bs4 import BeautifulSoup

# For performing regex operations
import re

# Data visualization
import seaborn as sns
import matplotlib.pyplot as plt

```

For this kickoff, we'll be scraping the **random functions names and usages** from Python documentation from the website [docs.python.org](https://docs.python.org/).

### Scrape The Data



```python
# Save the URL of the webpage we want to scrape to a variable
url = 'https://docs.python.org/3/library/random.html#module-random'
```

When web scraping, the first step is to pull down the content of the page into a Python (string) variable. For simpler webscraping tasks you can do this with the `requests` package, which is what we'll use here. For more complex tasks (involving, e.g., webpages with lots of Javascript or other elements that are rendered by the web browser) you may need to use something more advanced, like `urllib` or [Selenium](https://selenium-python.readthedocs.io/index.html).


```python
# Send a get request and assign the response to a variable
response = requests.get(url)
```

Let's take a look at what we have!


```python
response
```




    <Response [200]>




```python
response.content
```




<<<<<<< HEAD
    b'\n<!DOCTYPE html>\n\n<html xmlns="http://www.w3.org/1999/xhtml">\n  <head>\n    <meta charset="utf-8" />\n    <title>random \xe2\x80\x94 Generate pseudo-random numbers &#8212; Python 3.9.2 documentation</title>\n    <link rel="stylesheet" href="../_static/pydoctheme.css" type="text/css" />\n    <link rel="stylesheet" href="../_static/pygments.css" type="text/css" />\n    \n    <script id="documentation_options" data-url_root="../" src="../_static/documentation_options.js"></script>\n    <script src="../_static/jquery.js"></script>\n    <script src="../_static/underscore.js"></script>\n    <script src="../_static/doctools.js"></script>\n    <script src="../_static/language_data.js"></script>\n    \n    <script src="../_static/sidebar.js"></script>\n    \n    <link rel="search" type="application/opensearchdescription+xml"\n          title="Search within Python 3.9.2 documentation"\n          href="../_static/opensearch.xml"/>\n    <link rel="author" title="About these documents" href="../about.html" />\n    <link rel="index" title="Index" href="../genindex.html" />\n    <link rel="search" title="Search" href="../search.html" />\n    <link rel="copyright" title="Copyright" href="../copyright.html" />\n    <link rel="next" title="statistics \xe2\x80\x94 Mathematical statistics functions" href="statistics.html" />\n    <link rel="prev" title="fractions \xe2\x80\x94 Rational numbers" href="fractions.html" />\n    <link rel="canonical" href="https://docs.python.org/3/library/random.html" />\n    \n      \n      \n    \n\n    \n    <style>\n      @media only screen {\n        table.full-width-table {\n            width: 100%;\n        }\n      }\n    </style>\n\n    <link rel="shortcut icon" type="image/png" href="../_static/py.png" />\n    \n    <script type="text/javascript" src="../_static/copybutton.js"></script>\n    \n     \n\n\n  </head><body>\n  \n    <div class="related" role="navigation" aria-label="related navigation">\n      <h3>Navigation</h3>\n      <ul>\n        <li class="right" style="margin-right: 10px">\n          <a href="../genindex.html" title="General Index"\n             accesskey="I">index</a></li>\n        <li class="right" >\n          <a href="../py-modindex.html" title="Python Module Index"\n             >modules</a> |</li>\n        <li class="right" >\n          <a href="statistics.html" title="statistics \xe2\x80\x94 Mathematical statistics functions"\n             accesskey="N">next</a> |</li>\n        <li class="right" >\n          <a href="fractions.html" title="fractions \xe2\x80\x94 Rational numbers"\n             accesskey="P">previous</a> |</li>\n\n    <li><img src="../_static/py.png" alt=""\n             style="vertical-align: middle; margin-top: -1px"/></li>\n    <li><a href="https://www.python.org/">Python</a> &#187;</li>\n    \n\n    <li>\n      <a href="../index.html">3.9.2 Documentation</a> &#187;\n    </li>\n\n          <li class="nav-item nav-item-1"><a href="index.html" >The Python Standard Library</a> &#187;</li>\n          <li class="nav-item nav-item-2"><a href="numeric.html" accesskey="U">Numeric and Mathematical Modules</a> &#187;</li>\n    <li class="right">\n        \n\n    <div class="inline-search" style="display: none" role="search">\n        <form class="inline-search" action="../search.html" method="get">\n          <input placeholder="Quick search" type="text" name="q" />\n          <input type="submit" value="Go" />\n          <input type="hidden" name="check_keywords" value="yes" />\n          <input type="hidden" name="area" value="default" />\n        </form>\n    </div>\n    <script type="text/javascript">$(\'.inline-search\').show(0);</script>\n         |\n    </li>\n\n      </ul>\n    </div>    \n\n    <div class="document">\n      <div class="documentwrapper">\n        <div class="bodywrapper">\n          <div class="body" role="main">\n            \n  <div class="section" id="module-random">\n<span id="random-generate-pseudo-random-numbers"></span><h1><a class="reference internal" href="#module-random" title="random: Generate pseudo-random numbers with various common distributions."><code class="xref py py-mod docutils literal notranslate"><span class="pre">random</span></code></a> \xe2\x80\x94 Generate pseudo-random numbers<a class="headerlink" href="#module-random" title="Permalink to this headline">\xc2\xb6</a></h1>\n<p><strong>Source code:</strong> <a class="reference external" href="https://github.com/python/cpython/tree/3.9/Lib/random.py">Lib/random.py</a></p>\n<hr class="docutils" />\n<p>This module implements pseudo-random number generators for various\ndistributions.</p>\n<p>For integers, there is uniform selection from a range. For sequences, there is\nuniform selection of a random element, a function to generate a random\npermutation of a list in-place, and a function for random sampling without\nreplacement.</p>\n<p>On the real line, there are functions to compute uniform, normal (Gaussian),\nlognormal, negative exponential, gamma, and beta distributions. For generating\ndistributions of angles, the von Mises distribution is available.</p>\n<p>Almost all module functions depend on the basic function <a class="reference internal" href="#random.random" title="random.random"><code class="xref py py-func docutils literal notranslate"><span class="pre">random()</span></code></a>, which\ngenerates a random float uniformly in the semi-open range [0.0, 1.0).  Python\nuses the Mersenne Twister as the core generator.  It produces 53-bit precision\nfloats and has a period of 2**19937-1.  The underlying implementation in C is\nboth fast and threadsafe.  The Mersenne Twister is one of the most extensively\ntested random number generators in existence.  However, being completely\ndeterministic, it is not suitable for all purposes, and is completely unsuitable\nfor cryptographic purposes.</p>\n<p>The functions supplied by this module are actually bound methods of a hidden\ninstance of the <a class="reference internal" href="#random.Random" title="random.Random"><code class="xref py py-class docutils literal notranslate"><span class="pre">random.Random</span></code></a> class.  You can instantiate your own\ninstances of <a class="reference internal" href="#random.Random" title="random.Random"><code class="xref py py-class docutils literal notranslate"><span class="pre">Random</span></code></a> to get generators that don\xe2\x80\x99t share state.</p>\n<p>Class <a class="reference internal" href="#random.Random" title="random.Random"><code class="xref py py-class docutils literal notranslate"><span class="pre">Random</span></code></a> can also be subclassed if you want to use a different\nbasic generator of your own devising: in that case, override the <code class="xref py py-meth docutils literal notranslate"><span class="pre">random()</span></code>,\n<code class="xref py py-meth docutils literal notranslate"><span class="pre">seed()</span></code>, <code class="xref py py-meth docutils literal notranslate"><span class="pre">getstate()</span></code>, and <code class="xref py py-meth docutils literal notranslate"><span class="pre">setstate()</span></code> methods.\nOptionally, a new generator can supply a <code class="xref py py-meth docutils literal notranslate"><span class="pre">getrandbits()</span></code> method \xe2\x80\x94 this\nallows <a class="reference internal" href="#random.randrange" title="random.randrange"><code class="xref py py-meth docutils literal notranslate"><span class="pre">randrange()</span></code></a> to produce selections over an arbitrarily large range.</p>\n<p>The <a class="reference internal" href="#module-random" title="random: Generate pseudo-random numbers with various common distributions."><code class="xref py py-mod docutils literal notranslate"><span class="pre">random</span></code></a> module also provides the <a class="reference internal" href="#random.SystemRandom" title="random.SystemRandom"><code class="xref py py-class docutils literal notranslate"><span class="pre">SystemRandom</span></code></a> class which\nuses the system function <a class="reference internal" href="os.html#os.urandom" title="os.urandom"><code class="xref py py-func docutils literal notranslate"><span class="pre">os.urandom()</span></code></a> to generate random numbers\nfrom sources provided by the operating system.</p>\n<div class="admonition warning">\n<p class="admonition-title">Warning</p>\n<p>The pseudo-random generators of this module should not be used for\nsecurity purposes.  For security or cryptographic uses, see the\n<a class="reference internal" href="secrets.html#module-secrets" title="secrets: Generate secure random numbers for managing secrets."><code class="xref py py-mod docutils literal notranslate"><span class="pre">secrets</span></code></a> module.</p>\n</div>\n<div class="admonition seealso">\n<p class="admonition-title">See also</p>\n<p>M. Matsumoto and T. Nishimura, \xe2\x80\x9cMersenne Twister: A 623-dimensionally\nequidistributed uniform pseudorandom number generator\xe2\x80\x9d, ACM Transactions on\nModeling and Computer Simulation Vol. 8, No. 1, January pp.3\xe2\x80\x9330 1998.</p>\n<p><a class="reference external" href="https://code.activestate.com/recipes/576707/">Complementary-Multiply-with-Carry recipe</a> for a compatible alternative\nrandom number generator with a long period and comparatively simple update\noperations.</p>\n</div>\n<div class="section" id="bookkeeping-functions">\n<h2>Bookkeeping functions<a class="headerlink" href="#bookkeeping-functions" title="Permalink to this headline">\xc2\xb6</a></h2>\n<dl class="function">\n<dt id="random.seed">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">seed</code><span class="sig-paren">(</span><em class="sig-param">a=None</em>, <em class="sig-param">version=2</em><span class="sig-paren">)</span><a class="headerlink" href="#random.seed" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Initialize the random number generator.</p>\n<p>If <em>a</em> is omitted or <code class="docutils literal notranslate"><span class="pre">None</span></code>, the current system time is used.  If\nrandomness sources are provided by the operating system, they are used\ninstead of the system time (see the <a class="reference internal" href="os.html#os.urandom" title="os.urandom"><code class="xref py py-func docutils literal notranslate"><span class="pre">os.urandom()</span></code></a> function for details\non availability).</p>\n<p>If <em>a</em> is an int, it is used directly.</p>\n<p>With version 2 (the default), a <a class="reference internal" href="stdtypes.html#str" title="str"><code class="xref py py-class docutils literal notranslate"><span class="pre">str</span></code></a>, <a class="reference internal" href="stdtypes.html#bytes" title="bytes"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytes</span></code></a>, or <a class="reference internal" href="stdtypes.html#bytearray" title="bytearray"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytearray</span></code></a>\nobject gets converted to an <a class="reference internal" href="functions.html#int" title="int"><code class="xref py py-class docutils literal notranslate"><span class="pre">int</span></code></a> and all of its bits are used.</p>\n<p>With version 1 (provided for reproducing random sequences from older versions\nof Python), the algorithm for <a class="reference internal" href="stdtypes.html#str" title="str"><code class="xref py py-class docutils literal notranslate"><span class="pre">str</span></code></a> and <a class="reference internal" href="stdtypes.html#bytes" title="bytes"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytes</span></code></a> generates a\nnarrower range of seeds.</p>\n<div class="versionchanged">\n<p><span class="versionmodified changed">Changed in version 3.2: </span>Moved to the version 2 scheme which uses all of the bits in a string seed.</p>\n</div>\n<div class="deprecated">\n<p><span class="versionmodified deprecated">Deprecated since version 3.9: </span>In the future, the <em>seed</em> must be one of the following types:\n<em>NoneType</em>, <a class="reference internal" href="functions.html#int" title="int"><code class="xref py py-class docutils literal notranslate"><span class="pre">int</span></code></a>, <a class="reference internal" href="functions.html#float" title="float"><code class="xref py py-class docutils literal notranslate"><span class="pre">float</span></code></a>, <a class="reference internal" href="stdtypes.html#str" title="str"><code class="xref py py-class docutils literal notranslate"><span class="pre">str</span></code></a>,\n<a class="reference internal" href="stdtypes.html#bytes" title="bytes"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytes</span></code></a>, or <a class="reference internal" href="stdtypes.html#bytearray" title="bytearray"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytearray</span></code></a>.</p>\n</div>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.getstate">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">getstate</code><span class="sig-paren">(</span><span class="sig-paren">)</span><a class="headerlink" href="#random.getstate" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Return an object capturing the current internal state of the generator.  This\nobject can be passed to <a class="reference internal" href="#random.setstate" title="random.setstate"><code class="xref py py-func docutils literal notranslate"><span class="pre">setstate()</span></code></a> to restore the state.</p>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.setstate">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">setstate</code><span class="sig-paren">(</span><em class="sig-param">state</em><span class="sig-paren">)</span><a class="headerlink" href="#random.setstate" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p><em>state</em> should have been obtained from a previous call to <a class="reference internal" href="#random.getstate" title="random.getstate"><code class="xref py py-func docutils literal notranslate"><span class="pre">getstate()</span></code></a>, and\n<a class="reference internal" href="#random.setstate" title="random.setstate"><code class="xref py py-func docutils literal notranslate"><span class="pre">setstate()</span></code></a> restores the internal state of the generator to what it was at\nthe time <a class="reference internal" href="#random.getstate" title="random.getstate"><code class="xref py py-func docutils literal notranslate"><span class="pre">getstate()</span></code></a> was called.</p>\n</dd></dl>\n\n</div>\n<div class="section" id="functions-for-bytes">\n<h2>Functions for bytes<a class="headerlink" href="#functions-for-bytes" title="Permalink to this headline">\xc2\xb6</a></h2>\n<dl class="function">\n<dt id="random.randbytes">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">randbytes</code><span class="sig-paren">(</span><em class="sig-param">n</em><span class="sig-paren">)</span><a class="headerlink" href="#random.randbytes" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Generate <em>n</em> random bytes.</p>\n<p>This method should not be used for generating security tokens.\nUse <a class="reference internal" href="secrets.html#secrets.token_bytes" title="secrets.token_bytes"><code class="xref py py-func docutils literal notranslate"><span class="pre">secrets.token_bytes()</span></code></a> instead.</p>\n<div class="versionadded">\n<p><span class="versionmodified added">New in version 3.9.</span></p>\n</div>\n</dd></dl>\n\n</div>\n<div class="section" id="functions-for-integers">\n<h2>Functions for integers<a class="headerlink" href="#functions-for-integers" title="Permalink to this headline">\xc2\xb6</a></h2>\n<dl class="function">\n<dt id="random.randrange">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">randrange</code><span class="sig-paren">(</span><em class="sig-param">stop</em><span class="sig-paren">)</span><a class="headerlink" href="#random.randrange" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dt>\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">randrange</code><span class="sig-paren">(</span><em class="sig-param">start</em>, <em class="sig-param">stop</em><span class="optional">[</span>, <em class="sig-param">step</em><span class="optional">]</span><span class="sig-paren">)</span></dt>\n<dd><p>Return a randomly selected element from <code class="docutils literal notranslate"><span class="pre">range(start,</span> <span class="pre">stop,</span> <span class="pre">step)</span></code>.  This is\nequivalent to <code class="docutils literal notranslate"><span class="pre">choice(range(start,</span> <span class="pre">stop,</span> <span class="pre">step))</span></code>, but doesn\xe2\x80\x99t actually build a\nrange object.</p>\n<p>The positional argument pattern matches that of <a class="reference internal" href="stdtypes.html#range" title="range"><code class="xref py py-func docutils literal notranslate"><span class="pre">range()</span></code></a>.  Keyword arguments\nshould not be used because the function may use them in unexpected ways.</p>\n<div class="versionchanged">\n<p><span class="versionmodified changed">Changed in version 3.2: </span><a class="reference internal" href="#random.randrange" title="random.randrange"><code class="xref py py-meth docutils literal notranslate"><span class="pre">randrange()</span></code></a> is more sophisticated about producing equally distributed\nvalues.  Formerly it used a style like <code class="docutils literal notranslate"><span class="pre">int(random()*n)</span></code> which could produce\nslightly uneven distributions.</p>\n</div>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.randint">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">randint</code><span class="sig-paren">(</span><em class="sig-param">a</em>, <em class="sig-param">b</em><span class="sig-paren">)</span><a class="headerlink" href="#random.randint" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Return a random integer <em>N</em> such that <code class="docutils literal notranslate"><span class="pre">a</span> <span class="pre">&lt;=</span> <span class="pre">N</span> <span class="pre">&lt;=</span> <span class="pre">b</span></code>.  Alias for\n<code class="docutils literal notranslate"><span class="pre">randrange(a,</span> <span class="pre">b+1)</span></code>.</p>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.getrandbits">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">getrandbits</code><span class="sig-paren">(</span><em class="sig-param">k</em><span class="sig-paren">)</span><a class="headerlink" href="#random.getrandbits" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Returns a non-negative Python integer with <em>k</em> random bits. This method\nis supplied with the MersenneTwister generator and some other generators\nmay also provide it as an optional part of the API. When available,\n<a class="reference internal" href="#random.getrandbits" title="random.getrandbits"><code class="xref py py-meth docutils literal notranslate"><span class="pre">getrandbits()</span></code></a> enables <a class="reference internal" href="#random.randrange" title="random.randrange"><code class="xref py py-meth docutils literal notranslate"><span class="pre">randrange()</span></code></a> to handle arbitrarily large\nranges.</p>\n<div class="versionchanged">\n<p><span class="versionmodified changed">Changed in version 3.9: </span>This method now accepts zero for <em>k</em>.</p>\n</div>\n</dd></dl>\n\n</div>\n<div class="section" id="functions-for-sequences">\n<h2>Functions for sequences<a class="headerlink" href="#functions-for-sequences" title="Permalink to this headline">\xc2\xb6</a></h2>\n<dl class="function">\n<dt id="random.choice">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">choice</code><span class="sig-paren">(</span><em class="sig-param">seq</em><span class="sig-paren">)</span><a class="headerlink" href="#random.choice" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Return a random element from the non-empty sequence <em>seq</em>. If <em>seq</em> is empty,\nraises <a class="reference internal" href="exceptions.html#IndexError" title="IndexError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">IndexError</span></code></a>.</p>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.choices">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">choices</code><span class="sig-paren">(</span><em class="sig-param">population</em>, <em class="sig-param">weights=None</em>, <em class="sig-param">*</em>, <em class="sig-param">cum_weights=None</em>, <em class="sig-param">k=1</em><span class="sig-paren">)</span><a class="headerlink" href="#random.choices" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Return a <em>k</em> sized list of elements chosen from the <em>population</em> with replacement.\nIf the <em>population</em> is empty, raises <a class="reference internal" href="exceptions.html#IndexError" title="IndexError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">IndexError</span></code></a>.</p>\n<p>If a <em>weights</em> sequence is specified, selections are made according to the\nrelative weights.  Alternatively, if a <em>cum_weights</em> sequence is given, the\nselections are made according to the cumulative weights (perhaps computed\nusing <a class="reference internal" href="itertools.html#itertools.accumulate" title="itertools.accumulate"><code class="xref py py-func docutils literal notranslate"><span class="pre">itertools.accumulate()</span></code></a>).  For example, the relative weights\n<code class="docutils literal notranslate"><span class="pre">[10,</span> <span class="pre">5,</span> <span class="pre">30,</span> <span class="pre">5]</span></code> are equivalent to the cumulative weights\n<code class="docutils literal notranslate"><span class="pre">[10,</span> <span class="pre">15,</span> <span class="pre">45,</span> <span class="pre">50]</span></code>.  Internally, the relative weights are converted to\ncumulative weights before making selections, so supplying the cumulative\nweights saves work.</p>\n<p>If neither <em>weights</em> nor <em>cum_weights</em> are specified, selections are made\nwith equal probability.  If a weights sequence is supplied, it must be\nthe same length as the <em>population</em> sequence.  It is a <a class="reference internal" href="exceptions.html#TypeError" title="TypeError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">TypeError</span></code></a>\nto specify both <em>weights</em> and <em>cum_weights</em>.</p>\n<p>The <em>weights</em> or <em>cum_weights</em> can use any numeric type that interoperates\nwith the <a class="reference internal" href="functions.html#float" title="float"><code class="xref py py-class docutils literal notranslate"><span class="pre">float</span></code></a> values returned by <a class="reference internal" href="#module-random" title="random: Generate pseudo-random numbers with various common distributions."><code class="xref py py-func docutils literal notranslate"><span class="pre">random()</span></code></a> (that includes\nintegers, floats, and fractions but excludes decimals).  Behavior is\nundefined if any weight is negative.  A <a class="reference internal" href="exceptions.html#ValueError" title="ValueError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">ValueError</span></code></a> is raised if all\nweights are zero.</p>\n<p>For a given seed, the <a class="reference internal" href="#random.choices" title="random.choices"><code class="xref py py-func docutils literal notranslate"><span class="pre">choices()</span></code></a> function with equal weighting\ntypically produces a different sequence than repeated calls to\n<a class="reference internal" href="#random.choice" title="random.choice"><code class="xref py py-func docutils literal notranslate"><span class="pre">choice()</span></code></a>.  The algorithm used by <a class="reference internal" href="#random.choices" title="random.choices"><code class="xref py py-func docutils literal notranslate"><span class="pre">choices()</span></code></a> uses floating\npoint arithmetic for internal consistency and speed.  The algorithm used\nby <a class="reference internal" href="#random.choice" title="random.choice"><code class="xref py py-func docutils literal notranslate"><span class="pre">choice()</span></code></a> defaults to integer arithmetic with repeated selections\nto avoid small biases from round-off error.</p>\n<div class="versionadded">\n<p><span class="versionmodified added">New in version 3.6.</span></p>\n</div>\n<div class="versionchanged">\n<p><span class="versionmodified changed">Changed in version 3.9: </span>Raises a <a class="reference internal" href="exceptions.html#ValueError" title="ValueError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">ValueError</span></code></a> if all weights are zero.</p>\n</div>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.shuffle">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">shuffle</code><span class="sig-paren">(</span><em class="sig-param">x</em><span class="optional">[</span>, <em class="sig-param">random</em><span class="optional">]</span><span class="sig-paren">)</span><a class="headerlink" href="#random.shuffle" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Shuffle the sequence <em>x</em> in place.</p>\n<p>The optional argument <em>random</em> is a 0-argument function returning a random\nfloat in [0.0, 1.0); by default, this is the function <a class="reference internal" href="#random.random" title="random.random"><code class="xref py py-func docutils literal notranslate"><span class="pre">random()</span></code></a>.</p>\n<p>To shuffle an immutable sequence and return a new shuffled list, use\n<code class="docutils literal notranslate"><span class="pre">sample(x,</span> <span class="pre">k=len(x))</span></code> instead.</p>\n<p>Note that even for small <code class="docutils literal notranslate"><span class="pre">len(x)</span></code>, the total number of permutations of <em>x</em>\ncan quickly grow larger than the period of most random number generators.\nThis implies that most permutations of a long sequence can never be\ngenerated.  For example, a sequence of length 2080 is the largest that\ncan fit within the period of the Mersenne Twister random number generator.</p>\n<div class="deprecated-removed">\n<p><span class="versionmodified">Deprecated since version 3.9, will be removed in version 3.11: </span>The optional parameter <em>random</em>.</p>\n</div>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.sample">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">sample</code><span class="sig-paren">(</span><em class="sig-param">population</em>, <em class="sig-param">k</em>, <em class="sig-param">*</em>, <em class="sig-param">counts=None</em><span class="sig-paren">)</span><a class="headerlink" href="#random.sample" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Return a <em>k</em> length list of unique elements chosen from the population sequence\nor set. Used for random sampling without replacement.</p>\n<p>Returns a new list containing elements from the population while leaving the\noriginal population unchanged.  The resulting list is in selection order so that\nall sub-slices will also be valid random samples.  This allows raffle winners\n(the sample) to be partitioned into grand prize and second place winners (the\nsubslices).</p>\n<p>Members of the population need not be <a class="reference internal" href="../glossary.html#term-hashable"><span class="xref std std-term">hashable</span></a> or unique.  If the population\ncontains repeats, then each occurrence is a possible selection in the sample.</p>\n<p>Repeated elements can be specified one at a time or with the optional\nkeyword-only <em>counts</em> parameter.  For example, <code class="docutils literal notranslate"><span class="pre">sample([\'red\',</span> <span class="pre">\'blue\'],</span>\n<span class="pre">counts=[4,</span> <span class="pre">2],</span> <span class="pre">k=5)</span></code> is equivalent to <code class="docutils literal notranslate"><span class="pre">sample([\'red\',</span> <span class="pre">\'red\',</span> <span class="pre">\'red\',</span> <span class="pre">\'red\',</span>\n<span class="pre">\'blue\',</span> <span class="pre">\'blue\'],</span> <span class="pre">k=5)</span></code>.</p>\n<p>To choose a sample from a range of integers, use a <a class="reference internal" href="stdtypes.html#range" title="range"><code class="xref py py-func docutils literal notranslate"><span class="pre">range()</span></code></a> object as an\nargument.  This is especially fast and space efficient for sampling from a large\npopulation:  <code class="docutils literal notranslate"><span class="pre">sample(range(10000000),</span> <span class="pre">k=60)</span></code>.</p>\n<p>If the sample size is larger than the population size, a <a class="reference internal" href="exceptions.html#ValueError" title="ValueError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">ValueError</span></code></a>\nis raised.</p>\n<div class="versionchanged">\n<p><span class="versionmodified changed">Changed in version 3.9: </span>Added the <em>counts</em> parameter.</p>\n</div>\n<div class="deprecated">\n<p><span class="versionmodified deprecated">Deprecated since version 3.9: </span>In the future, the <em>population</em> must be a sequence.  Instances of\n<a class="reference internal" href="stdtypes.html#set" title="set"><code class="xref py py-class docutils literal notranslate"><span class="pre">set</span></code></a> are no longer supported.  The set must first be converted\nto a <a class="reference internal" href="stdtypes.html#list" title="list"><code class="xref py py-class docutils literal notranslate"><span class="pre">list</span></code></a> or <a class="reference internal" href="stdtypes.html#tuple" title="tuple"><code class="xref py py-class docutils literal notranslate"><span class="pre">tuple</span></code></a>, preferably in a deterministic\norder so that the sample is reproducible.</p>\n</div>\n</dd></dl>\n\n</div>\n<div class="section" id="real-valued-distributions">\n<span id="id1"></span><h2>Real-valued distributions<a class="headerlink" href="#real-valued-distributions" title="Permalink to this headline">\xc2\xb6</a></h2>\n<p>The following functions generate specific real-valued distributions. Function\nparameters are named after the corresponding variables in the distribution\xe2\x80\x99s\nequation, as used in common mathematical practice; most of these equations can\nbe found in any statistics text.</p>\n<dl class="function">\n<dt id="random.random">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">random</code><span class="sig-paren">(</span><span class="sig-paren">)</span><a class="headerlink" href="#random.random" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Return the next random floating point number in the range [0.0, 1.0).</p>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.uniform">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">uniform</code><span class="sig-paren">(</span><em class="sig-param">a</em>, <em class="sig-param">b</em><span class="sig-paren">)</span><a class="headerlink" href="#random.uniform" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Return a random floating point number <em>N</em> such that <code class="docutils literal notranslate"><span class="pre">a</span> <span class="pre">&lt;=</span> <span class="pre">N</span> <span class="pre">&lt;=</span> <span class="pre">b</span></code> for\n<code class="docutils literal notranslate"><span class="pre">a</span> <span class="pre">&lt;=</span> <span class="pre">b</span></code> and <code class="docutils literal notranslate"><span class="pre">b</span> <span class="pre">&lt;=</span> <span class="pre">N</span> <span class="pre">&lt;=</span> <span class="pre">a</span></code> for <code class="docutils literal notranslate"><span class="pre">b</span> <span class="pre">&lt;</span> <span class="pre">a</span></code>.</p>\n<p>The end-point value <code class="docutils literal notranslate"><span class="pre">b</span></code> may or may not be included in the range\ndepending on floating-point rounding in the equation <code class="docutils literal notranslate"><span class="pre">a</span> <span class="pre">+</span> <span class="pre">(b-a)</span> <span class="pre">*</span> <span class="pre">random()</span></code>.</p>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.triangular">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">triangular</code><span class="sig-paren">(</span><em class="sig-param">low</em>, <em class="sig-param">high</em>, <em class="sig-param">mode</em><span class="sig-paren">)</span><a class="headerlink" href="#random.triangular" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Return a random floating point number <em>N</em> such that <code class="docutils literal notranslate"><span class="pre">low</span> <span class="pre">&lt;=</span> <span class="pre">N</span> <span class="pre">&lt;=</span> <span class="pre">high</span></code> and\nwith the specified <em>mode</em> between those bounds.  The <em>low</em> and <em>high</em> bounds\ndefault to zero and one.  The <em>mode</em> argument defaults to the midpoint\nbetween the bounds, giving a symmetric distribution.</p>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.betavariate">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">betavariate</code><span class="sig-paren">(</span><em class="sig-param">alpha</em>, <em class="sig-param">beta</em><span class="sig-paren">)</span><a class="headerlink" href="#random.betavariate" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Beta distribution.  Conditions on the parameters are <code class="docutils literal notranslate"><span class="pre">alpha</span> <span class="pre">&gt;</span> <span class="pre">0</span></code> and\n<code class="docutils literal notranslate"><span class="pre">beta</span> <span class="pre">&gt;</span> <span class="pre">0</span></code>. Returned values range between 0 and 1.</p>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.expovariate">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">expovariate</code><span class="sig-paren">(</span><em class="sig-param">lambd</em><span class="sig-paren">)</span><a class="headerlink" href="#random.expovariate" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Exponential distribution.  <em>lambd</em> is 1.0 divided by the desired\nmean.  It should be nonzero.  (The parameter would be called\n\xe2\x80\x9clambda\xe2\x80\x9d, but that is a reserved word in Python.)  Returned values\nrange from 0 to positive infinity if <em>lambd</em> is positive, and from\nnegative infinity to 0 if <em>lambd</em> is negative.</p>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.gammavariate">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">gammavariate</code><span class="sig-paren">(</span><em class="sig-param">alpha</em>, <em class="sig-param">beta</em><span class="sig-paren">)</span><a class="headerlink" href="#random.gammavariate" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Gamma distribution.  (<em>Not</em> the gamma function!)  Conditions on the\nparameters are <code class="docutils literal notranslate"><span class="pre">alpha</span> <span class="pre">&gt;</span> <span class="pre">0</span></code> and <code class="docutils literal notranslate"><span class="pre">beta</span> <span class="pre">&gt;</span> <span class="pre">0</span></code>.</p>\n<p>The probability distribution function is:</p>\n<div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span>          <span class="n">x</span> <span class="o">**</span> <span class="p">(</span><span class="n">alpha</span> <span class="o">-</span> <span class="mi">1</span><span class="p">)</span> <span class="o">*</span> <span class="n">math</span><span class="o">.</span><span class="n">exp</span><span class="p">(</span><span class="o">-</span><span class="n">x</span> <span class="o">/</span> <span class="n">beta</span><span class="p">)</span>\n<span class="n">pdf</span><span class="p">(</span><span class="n">x</span><span class="p">)</span> <span class="o">=</span>  <span class="o">--------------------------------------</span>\n            <span class="n">math</span><span class="o">.</span><span class="n">gamma</span><span class="p">(</span><span class="n">alpha</span><span class="p">)</span> <span class="o">*</span> <span class="n">beta</span> <span class="o">**</span> <span class="n">alpha</span>\n</pre></div>\n</div>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.gauss">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">gauss</code><span class="sig-paren">(</span><em class="sig-param">mu</em>, <em class="sig-param">sigma</em><span class="sig-paren">)</span><a class="headerlink" href="#random.gauss" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Gaussian distribution.  <em>mu</em> is the mean, and <em>sigma</em> is the standard\ndeviation.  This is slightly faster than the <a class="reference internal" href="#random.normalvariate" title="random.normalvariate"><code class="xref py py-func docutils literal notranslate"><span class="pre">normalvariate()</span></code></a> function\ndefined below.</p>\n<p>Multithreading note:  When two threads call this function\nsimultaneously, it is possible that they will receive the\nsame return value.  This can be avoided in three ways.\n1) Have each thread use a different instance of the random\nnumber generator. 2) Put locks around all calls. 3) Use the\nslower, but thread-safe <a class="reference internal" href="#random.normalvariate" title="random.normalvariate"><code class="xref py py-func docutils literal notranslate"><span class="pre">normalvariate()</span></code></a> function instead.</p>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.lognormvariate">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">lognormvariate</code><span class="sig-paren">(</span><em class="sig-param">mu</em>, <em class="sig-param">sigma</em><span class="sig-paren">)</span><a class="headerlink" href="#random.lognormvariate" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Log normal distribution.  If you take the natural logarithm of this\ndistribution, you\xe2\x80\x99ll get a normal distribution with mean <em>mu</em> and standard\ndeviation <em>sigma</em>.  <em>mu</em> can have any value, and <em>sigma</em> must be greater than\nzero.</p>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.normalvariate">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">normalvariate</code><span class="sig-paren">(</span><em class="sig-param">mu</em>, <em class="sig-param">sigma</em><span class="sig-paren">)</span><a class="headerlink" href="#random.normalvariate" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Normal distribution.  <em>mu</em> is the mean, and <em>sigma</em> is the standard deviation.</p>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.vonmisesvariate">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">vonmisesvariate</code><span class="sig-paren">(</span><em class="sig-param">mu</em>, <em class="sig-param">kappa</em><span class="sig-paren">)</span><a class="headerlink" href="#random.vonmisesvariate" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p><em>mu</em> is the mean angle, expressed in radians between 0 and 2*<em>pi</em>, and <em>kappa</em>\nis the concentration parameter, which must be greater than or equal to zero.  If\n<em>kappa</em> is equal to zero, this distribution reduces to a uniform random angle\nover the range 0 to 2*<em>pi</em>.</p>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.paretovariate">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">paretovariate</code><span class="sig-paren">(</span><em class="sig-param">alpha</em><span class="sig-paren">)</span><a class="headerlink" href="#random.paretovariate" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Pareto distribution.  <em>alpha</em> is the shape parameter.</p>\n</dd></dl>\n\n<dl class="function">\n<dt id="random.weibullvariate">\n<code class="sig-prename descclassname">random.</code><code class="sig-name descname">weibullvariate</code><span class="sig-paren">(</span><em class="sig-param">alpha</em>, <em class="sig-param">beta</em><span class="sig-paren">)</span><a class="headerlink" href="#random.weibullvariate" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Weibull distribution.  <em>alpha</em> is the scale parameter and <em>beta</em> is the shape\nparameter.</p>\n</dd></dl>\n\n</div>\n<div class="section" id="alternative-generator">\n<h2>Alternative Generator<a class="headerlink" href="#alternative-generator" title="Permalink to this headline">\xc2\xb6</a></h2>\n<dl class="class">\n<dt id="random.Random">\n<em class="property">class </em><code class="sig-prename descclassname">random.</code><code class="sig-name descname">Random</code><span class="sig-paren">(</span><span class="optional">[</span><em class="sig-param">seed</em><span class="optional">]</span><span class="sig-paren">)</span><a class="headerlink" href="#random.Random" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Class that implements the default pseudo-random number generator used by the\n<a class="reference internal" href="#module-random" title="random: Generate pseudo-random numbers with various common distributions."><code class="xref py py-mod docutils literal notranslate"><span class="pre">random</span></code></a> module.</p>\n<div class="deprecated">\n<p><span class="versionmodified deprecated">Deprecated since version 3.9: </span>In the future, the <em>seed</em> must be one of the following types:\n<code class="xref py py-class docutils literal notranslate"><span class="pre">NoneType</span></code>, <a class="reference internal" href="functions.html#int" title="int"><code class="xref py py-class docutils literal notranslate"><span class="pre">int</span></code></a>, <a class="reference internal" href="functions.html#float" title="float"><code class="xref py py-class docutils literal notranslate"><span class="pre">float</span></code></a>, <a class="reference internal" href="stdtypes.html#str" title="str"><code class="xref py py-class docutils literal notranslate"><span class="pre">str</span></code></a>,\n<a class="reference internal" href="stdtypes.html#bytes" title="bytes"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytes</span></code></a>, or <a class="reference internal" href="stdtypes.html#bytearray" title="bytearray"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytearray</span></code></a>.</p>\n</div>\n</dd></dl>\n\n<dl class="class">\n<dt id="random.SystemRandom">\n<em class="property">class </em><code class="sig-prename descclassname">random.</code><code class="sig-name descname">SystemRandom</code><span class="sig-paren">(</span><span class="optional">[</span><em class="sig-param">seed</em><span class="optional">]</span><span class="sig-paren">)</span><a class="headerlink" href="#random.SystemRandom" title="Permalink to this definition">\xc2\xb6</a></dt>\n<dd><p>Class that uses the <a class="reference internal" href="os.html#os.urandom" title="os.urandom"><code class="xref py py-func docutils literal notranslate"><span class="pre">os.urandom()</span></code></a> function for generating random numbers\nfrom sources provided by the operating system. Not available on all systems.\nDoes not rely on software state, and sequences are not reproducible. Accordingly,\nthe <a class="reference internal" href="#random.seed" title="random.seed"><code class="xref py py-meth docutils literal notranslate"><span class="pre">seed()</span></code></a> method has no effect and is ignored.\nThe <a class="reference internal" href="#random.getstate" title="random.getstate"><code class="xref py py-meth docutils literal notranslate"><span class="pre">getstate()</span></code></a> and <a class="reference internal" href="#random.setstate" title="random.setstate"><code class="xref py py-meth docutils literal notranslate"><span class="pre">setstate()</span></code></a> methods raise\n<a class="reference internal" href="exceptions.html#NotImplementedError" title="NotImplementedError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">NotImplementedError</span></code></a> if called.</p>\n</dd></dl>\n\n</div>\n<div class="section" id="notes-on-reproducibility">\n<h2>Notes on Reproducibility<a class="headerlink" href="#notes-on-reproducibility" title="Permalink to this headline">\xc2\xb6</a></h2>\n<p>Sometimes it is useful to be able to reproduce the sequences given by a\npseudo-random number generator.  By re-using a seed value, the same sequence should be\nreproducible from run to run as long as multiple threads are not running.</p>\n<p>Most of the random module\xe2\x80\x99s algorithms and seeding functions are subject to\nchange across Python versions, but two aspects are guaranteed not to change:</p>\n<ul class="simple">\n<li><p>If a new seeding method is added, then a backward compatible seeder will be\noffered.</p></li>\n<li><p>The generator\xe2\x80\x99s <code class="xref py py-meth docutils literal notranslate"><span class="pre">random()</span></code> method will continue to produce the same\nsequence when the compatible seeder is given the same seed.</p></li>\n</ul>\n</div>\n<div class="section" id="examples">\n<span id="random-examples"></span><h2>Examples<a class="headerlink" href="#examples" title="Permalink to this headline">\xc2\xb6</a></h2>\n<p>Basic examples:</p>\n<div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="gp">&gt;&gt;&gt; </span><span class="n">random</span><span class="p">()</span>                             <span class="c1"># Random float:  0.0 &lt;= x &lt; 1.0</span>\n<span class="go">0.37444887175646646</span>\n\n<span class="gp">&gt;&gt;&gt; </span><span class="n">uniform</span><span class="p">(</span><span class="mf">2.5</span><span class="p">,</span> <span class="mf">10.0</span><span class="p">)</span>                   <span class="c1"># Random float:  2.5 &lt;= x &lt; 10.0</span>\n<span class="go">3.1800146073117523</span>\n\n<span class="gp">&gt;&gt;&gt; </span><span class="n">expovariate</span><span class="p">(</span><span class="mi">1</span> <span class="o">/</span> <span class="mi">5</span><span class="p">)</span>                   <span class="c1"># Interval between arrivals averaging 5 seconds</span>\n<span class="go">5.148957571865031</span>\n\n<span class="gp">&gt;&gt;&gt; </span><span class="n">randrange</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span>                        <span class="c1"># Integer from 0 to 9 inclusive</span>\n<span class="go">7</span>\n\n<span class="gp">&gt;&gt;&gt; </span><span class="n">randrange</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">101</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span>                 <span class="c1"># Even integer from 0 to 100 inclusive</span>\n<span class="go">26</span>\n\n<span class="gp">&gt;&gt;&gt; </span><span class="n">choice</span><span class="p">([</span><span class="s1">&#39;win&#39;</span><span class="p">,</span> <span class="s1">&#39;lose&#39;</span><span class="p">,</span> <span class="s1">&#39;draw&#39;</span><span class="p">])</span>      <span class="c1"># Single random element from a sequence</span>\n<span class="go">&#39;draw&#39;</span>\n\n<span class="gp">&gt;&gt;&gt; </span><span class="n">deck</span> <span class="o">=</span> <span class="s1">&#39;ace two three four&#39;</span><span class="o">.</span><span class="n">split</span><span class="p">()</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="n">shuffle</span><span class="p">(</span><span class="n">deck</span><span class="p">)</span>                        <span class="c1"># Shuffle a list</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="n">deck</span>\n<span class="go">[&#39;four&#39;, &#39;two&#39;, &#39;ace&#39;, &#39;three&#39;]</span>\n\n<span class="gp">&gt;&gt;&gt; </span><span class="n">sample</span><span class="p">([</span><span class="mi">10</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">30</span><span class="p">,</span> <span class="mi">40</span><span class="p">,</span> <span class="mi">50</span><span class="p">],</span> <span class="n">k</span><span class="o">=</span><span class="mi">4</span><span class="p">)</span>    <span class="c1"># Four samples without replacement</span>\n<span class="go">[40, 10, 50, 30]</span>\n</pre></div>\n</div>\n<p>Simulations:</p>\n<div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="gp">&gt;&gt;&gt; </span><span class="c1"># Six roulette wheel spins (weighted sampling with replacement)</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="n">choices</span><span class="p">([</span><span class="s1">&#39;red&#39;</span><span class="p">,</span> <span class="s1">&#39;black&#39;</span><span class="p">,</span> <span class="s1">&#39;green&#39;</span><span class="p">],</span> <span class="p">[</span><span class="mi">18</span><span class="p">,</span> <span class="mi">18</span><span class="p">,</span> <span class="mi">2</span><span class="p">],</span> <span class="n">k</span><span class="o">=</span><span class="mi">6</span><span class="p">)</span>\n<span class="go">[&#39;red&#39;, &#39;green&#39;, &#39;black&#39;, &#39;black&#39;, &#39;red&#39;, &#39;black&#39;]</span>\n\n<span class="gp">&gt;&gt;&gt; </span><span class="c1"># Deal 20 cards without replacement from a deck</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="c1"># of 52 playing cards, and determine the proportion of cards</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="c1"># with a ten-value:  ten, jack, queen, or king.</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="n">dealt</span> <span class="o">=</span> <span class="n">sample</span><span class="p">([</span><span class="s1">&#39;tens&#39;</span><span class="p">,</span> <span class="s1">&#39;low cards&#39;</span><span class="p">],</span> <span class="n">counts</span><span class="o">=</span><span class="p">[</span><span class="mi">16</span><span class="p">,</span> <span class="mi">36</span><span class="p">],</span> <span class="n">k</span><span class="o">=</span><span class="mi">20</span><span class="p">)</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="n">dealt</span><span class="o">.</span><span class="n">count</span><span class="p">(</span><span class="s1">&#39;tens&#39;</span><span class="p">)</span> <span class="o">/</span> <span class="mi">20</span>\n<span class="go">0.15</span>\n\n<span class="gp">&gt;&gt;&gt; </span><span class="c1"># Estimate the probability of getting 5 or more heads from 7 spins</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="c1"># of a biased coin that settles on heads 60% of the time.</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="k">def</span> <span class="nf">trial</span><span class="p">():</span>\n<span class="gp">... </span>    <span class="k">return</span> <span class="n">choices</span><span class="p">(</span><span class="s1">&#39;HT&#39;</span><span class="p">,</span> <span class="n">cum_weights</span><span class="o">=</span><span class="p">(</span><span class="mf">0.60</span><span class="p">,</span> <span class="mf">1.00</span><span class="p">),</span> <span class="n">k</span><span class="o">=</span><span class="mi">7</span><span class="p">)</span><span class="o">.</span><span class="n">count</span><span class="p">(</span><span class="s1">&#39;H&#39;</span><span class="p">)</span> <span class="o">&gt;=</span> <span class="mi">5</span>\n<span class="gp">...</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="nb">sum</span><span class="p">(</span><span class="n">trial</span><span class="p">()</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">10_000</span><span class="p">))</span> <span class="o">/</span> <span class="mi">10_000</span>\n<span class="go">0.4169</span>\n\n<span class="gp">&gt;&gt;&gt; </span><span class="c1"># Probability of the median of 5 samples being in middle two quartiles</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="k">def</span> <span class="nf">trial</span><span class="p">():</span>\n<span class="gp">... </span>    <span class="k">return</span> <span class="mi">2_500</span> <span class="o">&lt;=</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">choices</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="mi">10_000</span><span class="p">),</span> <span class="n">k</span><span class="o">=</span><span class="mi">5</span><span class="p">))[</span><span class="mi">2</span><span class="p">]</span> <span class="o">&lt;</span> <span class="mi">7_500</span>\n<span class="gp">...</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="nb">sum</span><span class="p">(</span><span class="n">trial</span><span class="p">()</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">10_000</span><span class="p">))</span> <span class="o">/</span> <span class="mi">10_000</span>\n<span class="go">0.7958</span>\n</pre></div>\n</div>\n<p>Example of <a class="reference external" href="https://en.wikipedia.org/wiki/Bootstrapping_(statistics)">statistical bootstrapping</a> using resampling\nwith replacement to estimate a confidence interval for the mean of a sample:</p>\n<div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="c1"># http://statistics.about.com/od/Applications/a/Example-Of-Bootstrapping.htm</span>\n<span class="kn">from</span> <span class="nn">statistics</span> <span class="kn">import</span> <span class="n">fmean</span> <span class="k">as</span> <span class="n">mean</span>\n<span class="kn">from</span> <span class="nn">random</span> <span class="kn">import</span> <span class="n">choices</span>\n\n<span class="n">data</span> <span class="o">=</span> <span class="p">[</span><span class="mi">41</span><span class="p">,</span> <span class="mi">50</span><span class="p">,</span> <span class="mi">29</span><span class="p">,</span> <span class="mi">37</span><span class="p">,</span> <span class="mi">81</span><span class="p">,</span> <span class="mi">30</span><span class="p">,</span> <span class="mi">73</span><span class="p">,</span> <span class="mi">63</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">35</span><span class="p">,</span> <span class="mi">68</span><span class="p">,</span> <span class="mi">22</span><span class="p">,</span> <span class="mi">60</span><span class="p">,</span> <span class="mi">31</span><span class="p">,</span> <span class="mi">95</span><span class="p">]</span>\n<span class="n">means</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">mean</span><span class="p">(</span><span class="n">choices</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">k</span><span class="o">=</span><span class="nb">len</span><span class="p">(</span><span class="n">data</span><span class="p">)))</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">100</span><span class="p">))</span>\n<span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">&#39;The sample mean of </span><span class="si">{</span><span class="n">mean</span><span class="p">(</span><span class="n">data</span><span class="p">)</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1"> has a 90% confidence &#39;</span>\n      <span class="sa">f</span><span class="s1">&#39;interval from </span><span class="si">{</span><span class="n">means</span><span class="p">[</span><span class="mi">5</span><span class="p">]</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1"> to </span><span class="si">{</span><span class="n">means</span><span class="p">[</span><span class="mi">94</span><span class="p">]</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1">&#39;</span><span class="p">)</span>\n</pre></div>\n</div>\n<p>Example of a <a class="reference external" href="https://en.wikipedia.org/wiki/Resampling_(statistics)#Permutation_tests">resampling permutation test</a>\nto determine the statistical significance or <a class="reference external" href="https://en.wikipedia.org/wiki/P-value">p-value</a> of an observed difference\nbetween the effects of a drug versus a placebo:</p>\n<div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="c1"># Example from &quot;Statistics is Easy&quot; by Dennis Shasha and Manda Wilson</span>\n<span class="kn">from</span> <span class="nn">statistics</span> <span class="kn">import</span> <span class="n">fmean</span> <span class="k">as</span> <span class="n">mean</span>\n<span class="kn">from</span> <span class="nn">random</span> <span class="kn">import</span> <span class="n">shuffle</span>\n\n<span class="n">drug</span> <span class="o">=</span> <span class="p">[</span><span class="mi">54</span><span class="p">,</span> <span class="mi">73</span><span class="p">,</span> <span class="mi">53</span><span class="p">,</span> <span class="mi">70</span><span class="p">,</span> <span class="mi">73</span><span class="p">,</span> <span class="mi">68</span><span class="p">,</span> <span class="mi">52</span><span class="p">,</span> <span class="mi">65</span><span class="p">,</span> <span class="mi">65</span><span class="p">]</span>\n<span class="n">placebo</span> <span class="o">=</span> <span class="p">[</span><span class="mi">54</span><span class="p">,</span> <span class="mi">51</span><span class="p">,</span> <span class="mi">58</span><span class="p">,</span> <span class="mi">44</span><span class="p">,</span> <span class="mi">55</span><span class="p">,</span> <span class="mi">52</span><span class="p">,</span> <span class="mi">42</span><span class="p">,</span> <span class="mi">47</span><span class="p">,</span> <span class="mi">58</span><span class="p">,</span> <span class="mi">46</span><span class="p">]</span>\n<span class="n">observed_diff</span> <span class="o">=</span> <span class="n">mean</span><span class="p">(</span><span class="n">drug</span><span class="p">)</span> <span class="o">-</span> <span class="n">mean</span><span class="p">(</span><span class="n">placebo</span><span class="p">)</span>\n\n<span class="n">n</span> <span class="o">=</span> <span class="mi">10_000</span>\n<span class="n">count</span> <span class="o">=</span> <span class="mi">0</span>\n<span class="n">combined</span> <span class="o">=</span> <span class="n">drug</span> <span class="o">+</span> <span class="n">placebo</span>\n<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n</span><span class="p">):</span>\n    <span class="n">shuffle</span><span class="p">(</span><span class="n">combined</span><span class="p">)</span>\n    <span class="n">new_diff</span> <span class="o">=</span> <span class="n">mean</span><span class="p">(</span><span class="n">combined</span><span class="p">[:</span><span class="nb">len</span><span class="p">(</span><span class="n">drug</span><span class="p">)])</span> <span class="o">-</span> <span class="n">mean</span><span class="p">(</span><span class="n">combined</span><span class="p">[</span><span class="nb">len</span><span class="p">(</span><span class="n">drug</span><span class="p">):])</span>\n    <span class="n">count</span> <span class="o">+=</span> <span class="p">(</span><span class="n">new_diff</span> <span class="o">&gt;=</span> <span class="n">observed_diff</span><span class="p">)</span>\n\n<span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">&#39;</span><span class="si">{</span><span class="n">n</span><span class="si">}</span><span class="s1"> label reshufflings produced only </span><span class="si">{</span><span class="n">count</span><span class="si">}</span><span class="s1"> instances with a difference&#39;</span><span class="p">)</span>\n<span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">&#39;at least as extreme as the observed difference of </span><span class="si">{</span><span class="n">observed_diff</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1">.&#39;</span><span class="p">)</span>\n<span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">&#39;The one-sided p-value of </span><span class="si">{</span><span class="n">count</span> <span class="o">/</span> <span class="n">n</span><span class="si">:</span><span class="s1">.4f</span><span class="si">}</span><span class="s1"> leads us to reject the null&#39;</span><span class="p">)</span>\n<span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">&#39;hypothesis that there is no difference between the drug and the placebo.&#39;</span><span class="p">)</span>\n</pre></div>\n</div>\n<p>Simulation of arrival times and service deliveries for a multiserver queue:</p>\n<div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="kn">from</span> <span class="nn">heapq</span> <span class="kn">import</span> <span class="n">heappush</span><span class="p">,</span> <span class="n">heappop</span>\n<span class="kn">from</span> <span class="nn">random</span> <span class="kn">import</span> <span class="n">expovariate</span><span class="p">,</span> <span class="n">gauss</span>\n<span class="kn">from</span> <span class="nn">statistics</span> <span class="kn">import</span> <span class="n">mean</span><span class="p">,</span> <span class="n">median</span><span class="p">,</span> <span class="n">stdev</span>\n\n<span class="n">average_arrival_interval</span> <span class="o">=</span> <span class="mf">5.6</span>\n<span class="n">average_service_time</span> <span class="o">=</span> <span class="mf">15.0</span>\n<span class="n">stdev_service_time</span> <span class="o">=</span> <span class="mf">3.5</span>\n<span class="n">num_servers</span> <span class="o">=</span> <span class="mi">3</span>\n\n<span class="n">waits</span> <span class="o">=</span> <span class="p">[]</span>\n<span class="n">arrival_time</span> <span class="o">=</span> <span class="mf">0.0</span>\n<span class="n">servers</span> <span class="o">=</span> <span class="p">[</span><span class="mf">0.0</span><span class="p">]</span> <span class="o">*</span> <span class="n">num_servers</span>  <span class="c1"># time when each server becomes available</span>\n<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">100_000</span><span class="p">):</span>\n    <span class="n">arrival_time</span> <span class="o">+=</span> <span class="n">expovariate</span><span class="p">(</span><span class="mf">1.0</span> <span class="o">/</span> <span class="n">average_arrival_interval</span><span class="p">)</span>\n    <span class="n">next_server_available</span> <span class="o">=</span> <span class="n">heappop</span><span class="p">(</span><span class="n">servers</span><span class="p">)</span>\n    <span class="n">wait</span> <span class="o">=</span> <span class="nb">max</span><span class="p">(</span><span class="mf">0.0</span><span class="p">,</span> <span class="n">next_server_available</span> <span class="o">-</span> <span class="n">arrival_time</span><span class="p">)</span>\n    <span class="n">waits</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">wait</span><span class="p">)</span>\n    <span class="n">service_duration</span> <span class="o">=</span> <span class="n">gauss</span><span class="p">(</span><span class="n">average_service_time</span><span class="p">,</span> <span class="n">stdev_service_time</span><span class="p">)</span>\n    <span class="n">service_completed</span> <span class="o">=</span> <span class="n">arrival_time</span> <span class="o">+</span> <span class="n">wait</span> <span class="o">+</span> <span class="n">service_duration</span>\n    <span class="n">heappush</span><span class="p">(</span><span class="n">servers</span><span class="p">,</span> <span class="n">service_completed</span><span class="p">)</span>\n\n<span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">&#39;Mean wait: </span><span class="si">{</span><span class="n">mean</span><span class="p">(</span><span class="n">waits</span><span class="p">)</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1">.  Stdev wait: </span><span class="si">{</span><span class="n">stdev</span><span class="p">(</span><span class="n">waits</span><span class="p">)</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1">.&#39;</span><span class="p">)</span>\n<span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">&#39;Median wait: </span><span class="si">{</span><span class="n">median</span><span class="p">(</span><span class="n">waits</span><span class="p">)</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1">.  Max wait: </span><span class="si">{</span><span class="nb">max</span><span class="p">(</span><span class="n">waits</span><span class="p">)</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1">.&#39;</span><span class="p">)</span>\n</pre></div>\n</div>\n<div class="admonition seealso">\n<p class="admonition-title">See also</p>\n<p><a class="reference external" href="https://www.youtube.com/watch?v=Iq9DzN6mvYA">Statistics for Hackers</a>\na video tutorial by\n<a class="reference external" href="https://us.pycon.org/2016/speaker/profile/295/">Jake Vanderplas</a>\non statistical analysis using just a few fundamental concepts\nincluding simulation, sampling, shuffling, and cross-validation.</p>\n<p><a class="reference external" href="http://nbviewer.jupyter.org/url/norvig.com/ipython/Economics.ipynb">Economics Simulation</a>\na simulation of a marketplace by\n<a class="reference external" href="http://norvig.com/bio.html">Peter Norvig</a> that shows effective\nuse of many of the tools and distributions provided by this module\n(gauss, uniform, sample, betavariate, choice, triangular, and randrange).</p>\n<p><a class="reference external" href="http://nbviewer.jupyter.org/url/norvig.com/ipython/Probability.ipynb">A Concrete Introduction to Probability (using Python)</a>\na tutorial by <a class="reference external" href="http://norvig.com/bio.html">Peter Norvig</a> covering\nthe basics of probability theory, how to write simulations, and\nhow to perform data analysis using Python.</p>\n</div>\n</div>\n<div class="section" id="recipes">\n<h2>Recipes<a class="headerlink" href="#recipes" title="Permalink to this headline">\xc2\xb6</a></h2>\n<p>The default <a class="reference internal" href="#random.random" title="random.random"><code class="xref py py-func docutils literal notranslate"><span class="pre">random()</span></code></a> returns multiples of 2\xe2\x81\xbb\xe2\x81\xb5\xc2\xb3 in the range\n<em>0.0 \xe2\x89\xa4 x &lt; 1.0</em>.  All such numbers are evenly spaced and are exactly\nrepresentable as Python floats.  However, many other representable\nfloats in that interval are not possible selections.  For example,\n<code class="docutils literal notranslate"><span class="pre">0.05954861408025609</span></code> isn\xe2\x80\x99t an integer multiple of 2\xe2\x81\xbb\xe2\x81\xb5\xc2\xb3.</p>\n<p>The following recipe takes a different approach.  All floats in the\ninterval are possible selections.  The mantissa comes from a uniform\ndistribution of integers in the range <em>2\xe2\x81\xb5\xc2\xb2 \xe2\x89\xa4 mantissa &lt; 2\xe2\x81\xb5\xc2\xb3</em>.  The\nexponent comes from a geometric distribution where exponents smaller\nthan <em>-53</em> occur half as often as the next larger exponent.</p>\n<div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="kn">from</span> <span class="nn">random</span> <span class="kn">import</span> <span class="n">Random</span>\n<span class="kn">from</span> <span class="nn">math</span> <span class="kn">import</span> <span class="n">ldexp</span>\n\n<span class="k">class</span> <span class="nc">FullRandom</span><span class="p">(</span><span class="n">Random</span><span class="p">):</span>\n\n    <span class="k">def</span> <span class="nf">random</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>\n        <span class="n">mantissa</span> <span class="o">=</span> <span class="mh">0x10_0000_0000_0000</span> <span class="o">|</span> <span class="bp">self</span><span class="o">.</span><span class="n">getrandbits</span><span class="p">(</span><span class="mi">52</span><span class="p">)</span>\n        <span class="n">exponent</span> <span class="o">=</span> <span class="o">-</span><span class="mi">53</span>\n        <span class="n">x</span> <span class="o">=</span> <span class="mi">0</span>\n        <span class="k">while</span> <span class="ow">not</span> <span class="n">x</span><span class="p">:</span>\n            <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">getrandbits</span><span class="p">(</span><span class="mi">32</span><span class="p">)</span>\n            <span class="n">exponent</span> <span class="o">+=</span> <span class="n">x</span><span class="o">.</span><span class="n">bit_length</span><span class="p">()</span> <span class="o">-</span> <span class="mi">32</span>\n        <span class="k">return</span> <span class="n">ldexp</span><span class="p">(</span><span class="n">mantissa</span><span class="p">,</span> <span class="n">exponent</span><span class="p">)</span>\n</pre></div>\n</div>\n<p>All <a class="reference internal" href="#real-valued-distributions"><span class="std std-ref">real valued distributions</span></a>\nin the class will use the new method:</p>\n<div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="gp">&gt;&gt;&gt; </span><span class="n">fr</span> <span class="o">=</span> <span class="n">FullRandom</span><span class="p">()</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="n">fr</span><span class="o">.</span><span class="n">random</span><span class="p">()</span>\n<span class="go">0.05954861408025609</span>\n<span class="gp">&gt;&gt;&gt; </span><span class="n">fr</span><span class="o">.</span><span class="n">expovariate</span><span class="p">(</span><span class="mf">0.25</span><span class="p">)</span>\n<span class="go">8.87925541791544</span>\n</pre></div>\n</div>\n<p>The recipe is conceptually equivalent to an algorithm that chooses from\nall the multiples of 2\xe2\x81\xbb\xc2\xb9\xe2\x81\xb0\xe2\x81\xb7\xe2\x81\xb4 in the range <em>0.0 \xe2\x89\xa4 x &lt; 1.0</em>.  All such\nnumbers are evenly spaced, but most have to be rounded down to the\nnearest representable Python float.  (The value 2\xe2\x81\xbb\xc2\xb9\xe2\x81\xb0\xe2\x81\xb7\xe2\x81\xb4 is the smallest\npositive unnormalized float and is equal to <code class="docutils literal notranslate"><span class="pre">math.ulp(0.0)</span></code>.)</p>\n<div class="admonition seealso">\n<p class="admonition-title">See also</p>\n<p><a class="reference external" href="https://allendowney.com/research/rand/downey07randfloat.pdf">Generating Pseudo-random Floating-Point Values</a> a\npaper by Allen B. Downey describing ways to generate more\nfine-grained floats than normally generated by <a class="reference internal" href="#random.random" title="random.random"><code class="xref py py-func docutils literal notranslate"><span class="pre">random()</span></code></a>.</p>\n</div>\n</div>\n</div>\n\n\n          </div>\n        </div>\n      </div>\n      <div class="sphinxsidebar" role="navigation" aria-label="main navigation">\n        <div class="sphinxsidebarwrapper">\n  <h3><a href="../contents.html">Table of Contents</a></h3>\n  <ul>\n<li><a class="reference internal" href="#"><code class="xref py py-mod docutils literal notranslate"><span class="pre">random</span></code> \xe2\x80\x94 Generate pseudo-random numbers</a><ul>\n<li><a class="reference internal" href="#bookkeeping-functions">Bookkeeping functions</a></li>\n<li><a class="reference internal" href="#functions-for-bytes">Functions for bytes</a></li>\n<li><a class="reference internal" href="#functions-for-integers">Functions for integers</a></li>\n<li><a class="reference internal" href="#functions-for-sequences">Functions for sequences</a></li>\n<li><a class="reference internal" href="#real-valued-distributions">Real-valued distributions</a></li>\n<li><a class="reference internal" href="#alternative-generator">Alternative Generator</a></li>\n<li><a class="reference internal" href="#notes-on-reproducibility">Notes on Reproducibility</a></li>\n<li><a class="reference internal" href="#examples">Examples</a></li>\n<li><a class="reference internal" href="#recipes">Recipes</a></li>\n</ul>\n</li>\n</ul>\n\n  <h4>Previous topic</h4>\n  <p class="topless"><a href="fractions.html"\n                        title="previous chapter"><code class="xref py py-mod docutils literal notranslate"><span class="pre">fractions</span></code> \xe2\x80\x94 Rational numbers</a></p>\n  <h4>Next topic</h4>\n  <p class="topless"><a href="statistics.html"\n                        title="next chapter"><code class="xref py py-mod docutils literal notranslate"><span class="pre">statistics</span></code> \xe2\x80\x94 Mathematical statistics functions</a></p>\n  <div role="note" aria-label="source link">\n    <h3>This Page</h3>\n    <ul class="this-page-menu">\n      <li><a href="../bugs.html">Report a Bug</a></li>\n      <li>\n        <a href="https://github.com/python/cpython/blob/master/Doc/library/random.rst"\n            rel="nofollow">Show Source\n        </a>\n      </li>\n    </ul>\n  </div>\n        </div>\n      </div>\n      <div class="clearer"></div>\n    </div>  \n    <div class="related" role="navigation" aria-label="related navigation">\n      <h3>Navigation</h3>\n      <ul>\n        <li class="right" style="margin-right: 10px">\n          <a href="../genindex.html" title="General Index"\n             >index</a></li>\n        <li class="right" >\n          <a href="../py-modindex.html" title="Python Module Index"\n             >modules</a> |</li>\n        <li class="right" >\n          <a href="statistics.html" title="statistics \xe2\x80\x94 Mathematical statistics functions"\n             >next</a> |</li>\n        <li class="right" >\n          <a href="fractions.html" title="fractions \xe2\x80\x94 Rational numbers"\n             >previous</a> |</li>\n\n    <li><img src="../_static/py.png" alt=""\n             style="vertical-align: middle; margin-top: -1px"/></li>\n    <li><a href="https://www.python.org/">Python</a> &#187;</li>\n    \n\n    <li>\n      <a href="../index.html">3.9.2 Documentation</a> &#187;\n    </li>\n\n          <li class="nav-item nav-item-1"><a href="index.html" >The Python Standard Library</a> &#187;</li>\n          <li class="nav-item nav-item-2"><a href="numeric.html" >Numeric and Mathematical Modules</a> &#187;</li>\n    <li class="right">\n        \n\n    <div class="inline-search" style="display: none" role="search">\n        <form class="inline-search" action="../search.html" method="get">\n          <input placeholder="Quick search" type="text" name="q" />\n          <input type="submit" value="Go" />\n          <input type="hidden" name="check_keywords" value="yes" />\n          <input type="hidden" name="area" value="default" />\n        </form>\n    </div>\n    <script type="text/javascript">$(\'.inline-search\').show(0);</script>\n         |\n    </li>\n\n      </ul>\n    </div>  \n    <div class="footer">\n    &copy; <a href="../copyright.html">Copyright</a> 2001-2021, Python Software Foundation.\n    <br />\n\n    The Python Software Foundation is a non-profit corporation.\n<a href="https://www.python.org/psf/donations/">Please donate.</a>\n<br />\n    <br />\n\n    Last updated on Mar 24, 2021.\n    <a href="https://docs.python.org/3/bugs.html">Found a bug</a>?\n    <br />\n\n    Created using <a href="https://www.sphinx-doc.org/">Sphinx</a> 2.4.4.\n    </div>\n\n    <script type="text/javascript" src="../_static/switchers.js"></script>\n  </body>\n</html>'
=======
    b'\n<!DOCTYPE html>\n\n<html xmlns="http://www.w3.org/1999/xhtml">\n  <head>\n    <meta charset="utf-8" />\n    <title>random \xe2\x80\x94 Generate pseudo-random numbers &#8212; Python 3.9.2 documentation</title>\n    <link rel="stylesheet" href="../_static/pydoctheme.css" type="text/css" />\n    <link rel="stylesheet" href="../_static/pygments.css" type="text/css" />\n    \n    <script id="documentation_options" data-url_root="../" src="../_static/documentation_options.js"></script>\n    <script src="../_static/jquery.js"></script>\n    <script src="../_static/underscore.js"></script>\n    <script src="../_static/doctools.js"></script>\n    <script src="../_static/language_data.js"></script>\n    \n    <script src="../_static/sidebar.js"></script>\n    \n    <link rel="search" type="application/opensearchdescription+xml"\n          title="Search within Python 3.9.2 documentation"\n          href="../_static/opensearch.xml"/>\n    <link rel="author" title="About these documents" href="../about.html" />\n    <link rel="index" title="Index" href="../genindex.html" />\n    <link rel="search" title="Search" href="../search.html" />\n    <link rel="copyright" title="Copyright" href="../copyright.html" />\n    <link rel="next" title="statistics \xe2\x80\x94 Mathematical statistics functions" href="statistics.html" />\n    <link rel="prev" title="fractions \xe2\x80\x94 Rational numbers" href="fractions.html" />\n    <link rel="canonical" href="https://docs.python.org/3/library/random.html" />\n    \n      \n      \n    \n\n    \n    <style>\n      @media only screen {\n        table.full-width-table {\n            width: 100%;\n        }\n      }\n    </style>\n\n    <link rel="shortcut icon" type="image/png" href="../_static/py.png" />\n    \n    <script type="text/javascript" src="../_static/copybutton.js"></script>\n    \n     \n\n\n  </head><body>\n  \n    <div class="related" role="navigation" aria-label="related navigation">\n      <h3>Navigation</h3>\n      <ul>\n        <li class="right" style="margin-right: 10px">\n          <a href="../genindex.html" title="General Index"\n             accesskey="I">index</a></li>\n        <li class="right" >\n          <a href="../py-modindex.html" title="Python Module Index"\n             >modules</a> |</li>\n        <li class="right" >\n          <a href="statistics.html" title="statistics \xe2\x80\x94 Mathematical statistics functions"\n             accesskey="N">next</a> |</li>\n        <li class="right" >\n          <a href="fractions.html" title="fractions \xe2\x80\x94 Rational numbers"\n             accesskey="P">previous</a> |</li>\n\n    <li><img src="../_static/py.png" alt=""\n             style="vertical-align: middle; margin-top: -1px"/></li>\n    <li><a href="https://www.python.org/">Python</a> &#187;</li>\n    \n\n    <li>\n      <a href="../index.html">3.9.2 Documentation</a> &#187;\n    </li>\n\n          <li class="nav-item nav-item-1"><a href="index.html" >The Python Standard Library</a> &#187;</li>\n          <li class="nav-item nav-item-2"><a href="numeric.html" accesskey="U">Numeric and Mathematical Modules</a> &#187;</li>\n    <li class="right">\n        \n\n    <div class="inline-search" style="display: none" role="search">\n        <form class="inline-search" action="../search.html" method="get">\n          <input placeholder="Quick search" type="text" name="q" />\n          <input type="submit" value="Go" />\n          <input type="hidden" name="check_keywords" value="yes" />\n          <input type="hidden" name="area" value="default" />\n        </form>\n    </div>\n    <script type="text/javascript">
>>>>>>> First commit



That's a lot to look at! It's also pretty unreadable. This is where Beautiful Soup comes in. What Beautiful Soup does is helps us parse the page content properly, into a form that we can more easily use.


```python
# Turn the undecoded content into a Beautiful Soup object and assign it to a variable
soup = BeautifulSoup(response.content)
type(soup)
```




    bs4.BeautifulSoup



**Now let's take a look at this.**


```python
# Check soup variable

soup
```




    <!DOCTYPE html>
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <meta charset="utf-8"/>
    <title>random — Generate pseudo-random numbers — Python 3.9.2 documentation</title>
    <link href="../_static/pydoctheme.css" rel="stylesheet" type="text/css"/>
    <link href="../_static/pygments.css" rel="stylesheet" type="text/css"/>
    <script data-url_root="../" id="documentation_options" src="../_static/documentation_options.js"></script>
    <script src="../_static/jquery.js"></script>
    <script src="../_static/underscore.js"></script>
    <script src="../_static/doctools.js"></script>
    <script src="../_static/language_data.js"></script>
    <script src="../_static/sidebar.js"></script>
    <link href="../_static/opensearch.xml" rel="search" title="Search within Python 3.9.2 documentation" type="application/opensearchdescription+xml"/>
    <link href="../about.html" rel="author" title="About these documents"/>
    <link href="../genindex.html" rel="index" title="Index"/>
    <link href="../search.html" rel="search" title="Search"/>
    <link href="../copyright.html" rel="copyright" title="Copyright"/>
    <link href="statistics.html" rel="next" title="statistics — Mathematical statistics functions"/>
    <link href="fractions.html" rel="prev" title="fractions — Rational numbers"/>
    <link href="https://docs.python.org/3/library/random.html" rel="canonical"/>
<<<<<<< HEAD
    <style>
          @media only screen {
            table.full-width-table {
                width: 100%;
            }
          }
        </style>
    <link href="../_static/py.png" rel="shortcut icon" type="image/png"/>
    <script src="../_static/copybutton.js" type="text/javascript"></script>
    </head><body>
    <div aria-label="related navigation" class="related" role="navigation">
    <h3>Navigation</h3>
    <ul>
    <li class="right" style="margin-right: 10px">
    <a accesskey="I" href="../genindex.html" title="General Index">index</a></li>
    <li class="right">
    <a href="../py-modindex.html" title="Python Module Index">modules</a> |</li>
    <li class="right">
    <a accesskey="N" href="statistics.html" title="statistics — Mathematical statistics functions">next</a> |</li>
    <li class="right">
    <a accesskey="P" href="fractions.html" title="fractions — Rational numbers">previous</a> |</li>
    <li><img alt="" src="../_static/py.png" style="vertical-align: middle; margin-top: -1px"/></li>
    <li><a href="https://www.python.org/">Python</a> »</li>
    <li>
    <a href="../index.html">3.9.2 Documentation</a> »
        </li>
    <li class="nav-item nav-item-1"><a href="index.html">The Python Standard Library</a> »</li>
    <li class="nav-item nav-item-2"><a accesskey="U" href="numeric.html">Numeric and Mathematical Modules</a> »</li>
    <li class="right">
    <div class="inline-search" role="search" style="display: none">
    <form action="../search.html" class="inline-search" method="get">
    <input name="q" placeholder="Quick search" type="text"/>
    <input type="submit" value="Go"/>
    <input name="check_keywords" type="hidden" value="yes"/>
    <input name="area" type="hidden" value="default"/>
    </form>
    </div>
    <script type="text/javascript">$('.inline-search').show(0);</script>
             |
        </li>
    </ul>
    </div>
    <div class="document">
    <div class="documentwrapper">
    <div class="bodywrapper">
    <div class="body" role="main">
    <div class="section" id="module-random">
    <span id="random-generate-pseudo-random-numbers"></span><h1><a class="reference internal" href="#module-random" title="random: Generate pseudo-random numbers with various common distributions."><code class="xref py py-mod docutils literal notranslate"><span class="pre">random</span></code></a> — Generate pseudo-random numbers<a class="headerlink" href="#module-random" title="Permalink to this headline">¶</a></h1>
    <p><strong>Source code:</strong> <a class="reference external" href="https://github.com/python/cpython/tree/3.9/Lib/random.py">Lib/random.py</a></p>
    <hr class="docutils"/>
    <p>This module implements pseudo-random number generators for various
    distributions.</p>
    <p>For integers, there is uniform selection from a range. For sequences, there is
    uniform selection of a random element, a function to generate a random
    permutation of a list in-place, and a function for random sampling without
    replacement.</p>
    <p>On the real line, there are functions to compute uniform, normal (Gaussian),
    lognormal, negative exponential, gamma, and beta distributions. For generating
    distributions of angles, the von Mises distribution is available.</p>
    <p>Almost all module functions depend on the basic function <a class="reference internal" href="#random.random" title="random.random"><code class="xref py py-func docutils literal notranslate"><span class="pre">random()</span></code></a>, which
    generates a random float uniformly in the semi-open range [0.0, 1.0).  Python
    uses the Mersenne Twister as the core generator.  It produces 53-bit precision
    floats and has a period of 2**19937-1.  The underlying implementation in C is
    both fast and threadsafe.  The Mersenne Twister is one of the most extensively
    tested random number generators in existence.  However, being completely
    deterministic, it is not suitable for all purposes, and is completely unsuitable
    for cryptographic purposes.</p>
    <p>The functions supplied by this module are actually bound methods of a hidden
    instance of the <a class="reference internal" href="#random.Random" title="random.Random"><code class="xref py py-class docutils literal notranslate"><span class="pre">random.Random</span></code></a> class.  You can instantiate your own
    instances of <a class="reference internal" href="#random.Random" title="random.Random"><code class="xref py py-class docutils literal notranslate"><span class="pre">Random</span></code></a> to get generators that don’t share state.</p>
    <p>Class <a class="reference internal" href="#random.Random" title="random.Random"><code class="xref py py-class docutils literal notranslate"><span class="pre">Random</span></code></a> can also be subclassed if you want to use a different
    basic generator of your own devising: in that case, override the <code class="xref py py-meth docutils literal notranslate"><span class="pre">random()</span></code>,
    <code class="xref py py-meth docutils literal notranslate"><span class="pre">seed()</span></code>, <code class="xref py py-meth docutils literal notranslate"><span class="pre">getstate()</span></code>, and <code class="xref py py-meth docutils literal notranslate"><span class="pre">setstate()</span></code> methods.
    Optionally, a new generator can supply a <code class="xref py py-meth docutils literal notranslate"><span class="pre">getrandbits()</span></code> method — this
    allows <a class="reference internal" href="#random.randrange" title="random.randrange"><code class="xref py py-meth docutils literal notranslate"><span class="pre">randrange()</span></code></a> to produce selections over an arbitrarily large range.</p>
    <p>The <a class="reference internal" href="#module-random" title="random: Generate pseudo-random numbers with various common distributions."><code class="xref py py-mod docutils literal notranslate"><span class="pre">random</span></code></a> module also provides the <a class="reference internal" href="#random.SystemRandom" title="random.SystemRandom"><code class="xref py py-class docutils literal notranslate"><span class="pre">SystemRandom</span></code></a> class which
    uses the system function <a class="reference internal" href="os.html#os.urandom" title="os.urandom"><code class="xref py py-func docutils literal notranslate"><span class="pre">os.urandom()</span></code></a> to generate random numbers
    from sources provided by the operating system.</p>
    <div class="admonition warning">
    <p class="admonition-title">Warning</p>
    <p>The pseudo-random generators of this module should not be used for
    security purposes.  For security or cryptographic uses, see the
    <a class="reference internal" href="secrets.html#module-secrets" title="secrets: Generate secure random numbers for managing secrets."><code class="xref py py-mod docutils literal notranslate"><span class="pre">secrets</span></code></a> module.</p>
    </div>
    <div class="admonition seealso">
    <p class="admonition-title">See also</p>
    <p>M. Matsumoto and T. Nishimura, “Mersenne Twister: A 623-dimensionally
    equidistributed uniform pseudorandom number generator”, ACM Transactions on
    Modeling and Computer Simulation Vol. 8, No. 1, January pp.3–30 1998.</p>
    <p><a class="reference external" href="https://code.activestate.com/recipes/576707/">Complementary-Multiply-with-Carry recipe</a> for a compatible alternative
    random number generator with a long period and comparatively simple update
    operations.</p>
    </div>
    <div class="section" id="bookkeeping-functions">
    <h2>Bookkeeping functions<a class="headerlink" href="#bookkeeping-functions" title="Permalink to this headline">¶</a></h2>
    <dl class="function">
    <dt id="random.seed">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">seed</code><span class="sig-paren">(</span><em class="sig-param">a=None</em>, <em class="sig-param">version=2</em><span class="sig-paren">)</span><a class="headerlink" href="#random.seed" title="Permalink to this definition">¶</a></dt>
    <dd><p>Initialize the random number generator.</p>
    <p>If <em>a</em> is omitted or <code class="docutils literal notranslate"><span class="pre">None</span></code>, the current system time is used.  If
    randomness sources are provided by the operating system, they are used
    instead of the system time (see the <a class="reference internal" href="os.html#os.urandom" title="os.urandom"><code class="xref py py-func docutils literal notranslate"><span class="pre">os.urandom()</span></code></a> function for details
    on availability).</p>
    <p>If <em>a</em> is an int, it is used directly.</p>
    <p>With version 2 (the default), a <a class="reference internal" href="stdtypes.html#str" title="str"><code class="xref py py-class docutils literal notranslate"><span class="pre">str</span></code></a>, <a class="reference internal" href="stdtypes.html#bytes" title="bytes"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytes</span></code></a>, or <a class="reference internal" href="stdtypes.html#bytearray" title="bytearray"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytearray</span></code></a>
    object gets converted to an <a class="reference internal" href="functions.html#int" title="int"><code class="xref py py-class docutils literal notranslate"><span class="pre">int</span></code></a> and all of its bits are used.</p>
    <p>With version 1 (provided for reproducing random sequences from older versions
    of Python), the algorithm for <a class="reference internal" href="stdtypes.html#str" title="str"><code class="xref py py-class docutils literal notranslate"><span class="pre">str</span></code></a> and <a class="reference internal" href="stdtypes.html#bytes" title="bytes"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytes</span></code></a> generates a
    narrower range of seeds.</p>
    <div class="versionchanged">
    <p><span class="versionmodified changed">Changed in version 3.2: </span>Moved to the version 2 scheme which uses all of the bits in a string seed.</p>
    </div>
    <div class="deprecated">
    <p><span class="versionmodified deprecated">Deprecated since version 3.9: </span>In the future, the <em>seed</em> must be one of the following types:
    <em>NoneType</em>, <a class="reference internal" href="functions.html#int" title="int"><code class="xref py py-class docutils literal notranslate"><span class="pre">int</span></code></a>, <a class="reference internal" href="functions.html#float" title="float"><code class="xref py py-class docutils literal notranslate"><span class="pre">float</span></code></a>, <a class="reference internal" href="stdtypes.html#str" title="str"><code class="xref py py-class docutils literal notranslate"><span class="pre">str</span></code></a>,
    <a class="reference internal" href="stdtypes.html#bytes" title="bytes"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytes</span></code></a>, or <a class="reference internal" href="stdtypes.html#bytearray" title="bytearray"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytearray</span></code></a>.</p>
    </div>
    </dd></dl>
    <dl class="function">
    <dt id="random.getstate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">getstate</code><span class="sig-paren">(</span><span class="sig-paren">)</span><a class="headerlink" href="#random.getstate" title="Permalink to this definition">¶</a></dt>
    <dd><p>Return an object capturing the current internal state of the generator.  This
    object can be passed to <a class="reference internal" href="#random.setstate" title="random.setstate"><code class="xref py py-func docutils literal notranslate"><span class="pre">setstate()</span></code></a> to restore the state.</p>
    </dd></dl>
    <dl class="function">
    <dt id="random.setstate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">setstate</code><span class="sig-paren">(</span><em class="sig-param">state</em><span class="sig-paren">)</span><a class="headerlink" href="#random.setstate" title="Permalink to this definition">¶</a></dt>
    <dd><p><em>state</em> should have been obtained from a previous call to <a class="reference internal" href="#random.getstate" title="random.getstate"><code class="xref py py-func docutils literal notranslate"><span class="pre">getstate()</span></code></a>, and
    <a class="reference internal" href="#random.setstate" title="random.setstate"><code class="xref py py-func docutils literal notranslate"><span class="pre">setstate()</span></code></a> restores the internal state of the generator to what it was at
    the time <a class="reference internal" href="#random.getstate" title="random.getstate"><code class="xref py py-func docutils literal notranslate"><span class="pre">getstate()</span></code></a> was called.</p>
    </dd></dl>
    </div>
    <div class="section" id="functions-for-bytes">
    <h2>Functions for bytes<a class="headerlink" href="#functions-for-bytes" title="Permalink to this headline">¶</a></h2>
    <dl class="function">
    <dt id="random.randbytes">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">randbytes</code><span class="sig-paren">(</span><em class="sig-param">n</em><span class="sig-paren">)</span><a class="headerlink" href="#random.randbytes" title="Permalink to this definition">¶</a></dt>
    <dd><p>Generate <em>n</em> random bytes.</p>
    <p>This method should not be used for generating security tokens.
    Use <a class="reference internal" href="secrets.html#secrets.token_bytes" title="secrets.token_bytes"><code class="xref py py-func docutils literal notranslate"><span class="pre">secrets.token_bytes()</span></code></a> instead.</p>
    <div class="versionadded">
    <p><span class="versionmodified added">New in version 3.9.</span></p>
    </div>
    </dd></dl>
    </div>
    <div class="section" id="functions-for-integers">
    <h2>Functions for integers<a class="headerlink" href="#functions-for-integers" title="Permalink to this headline">¶</a></h2>
    <dl class="function">
    <dt id="random.randrange">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">randrange</code><span class="sig-paren">(</span><em class="sig-param">stop</em><span class="sig-paren">)</span><a class="headerlink" href="#random.randrange" title="Permalink to this definition">¶</a></dt>
    <dt>
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">randrange</code><span class="sig-paren">(</span><em class="sig-param">start</em>, <em class="sig-param">stop</em><span class="optional">[</span>, <em class="sig-param">step</em><span class="optional">]</span><span class="sig-paren">)</span></dt>
    <dd><p>Return a randomly selected element from <code class="docutils literal notranslate"><span class="pre">range(start,</span> <span class="pre">stop,</span> <span class="pre">step)</span></code>.  This is
    equivalent to <code class="docutils literal notranslate"><span class="pre">choice(range(start,</span> <span class="pre">stop,</span> <span class="pre">step))</span></code>, but doesn’t actually build a
    range object.</p>
    <p>The positional argument pattern matches that of <a class="reference internal" href="stdtypes.html#range" title="range"><code class="xref py py-func docutils literal notranslate"><span class="pre">range()</span></code></a>.  Keyword arguments
    should not be used because the function may use them in unexpected ways.</p>
    <div class="versionchanged">
    <p><span class="versionmodified changed">Changed in version 3.2: </span><a class="reference internal" href="#random.randrange" title="random.randrange"><code class="xref py py-meth docutils literal notranslate"><span class="pre">randrange()</span></code></a> is more sophisticated about producing equally distributed
    values.  Formerly it used a style like <code class="docutils literal notranslate"><span class="pre">int(random()*n)</span></code> which could produce
    slightly uneven distributions.</p>
    </div>
    </dd></dl>
    <dl class="function">
    <dt id="random.randint">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">randint</code><span class="sig-paren">(</span><em class="sig-param">a</em>, <em class="sig-param">b</em><span class="sig-paren">)</span><a class="headerlink" href="#random.randint" title="Permalink to this definition">¶</a></dt>
    <dd><p>Return a random integer <em>N</em> such that <code class="docutils literal notranslate"><span class="pre">a</span> <span class="pre">&lt;=</span> <span class="pre">N</span> <span class="pre">&lt;=</span> <span class="pre">b</span></code>.  Alias for
    <code class="docutils literal notranslate"><span class="pre">randrange(a,</span> <span class="pre">b+1)</span></code>.</p>
    </dd></dl>
    <dl class="function">
    <dt id="random.getrandbits">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">getrandbits</code><span class="sig-paren">(</span><em class="sig-param">k</em><span class="sig-paren">)</span><a class="headerlink" href="#random.getrandbits" title="Permalink to this definition">¶</a></dt>
    <dd><p>Returns a non-negative Python integer with <em>k</em> random bits. This method
    is supplied with the MersenneTwister generator and some other generators
    may also provide it as an optional part of the API. When available,
    <a class="reference internal" href="#random.getrandbits" title="random.getrandbits"><code class="xref py py-meth docutils literal notranslate"><span class="pre">getrandbits()</span></code></a> enables <a class="reference internal" href="#random.randrange" title="random.randrange"><code class="xref py py-meth docutils literal notranslate"><span class="pre">randrange()</span></code></a> to handle arbitrarily large
    ranges.</p>
    <div class="versionchanged">
    <p><span class="versionmodified changed">Changed in version 3.9: </span>This method now accepts zero for <em>k</em>.</p>
    </div>
    </dd></dl>
    </div>
    <div class="section" id="functions-for-sequences">
    <h2>Functions for sequences<a class="headerlink" href="#functions-for-sequences" title="Permalink to this headline">¶</a></h2>
    <dl class="function">
    <dt id="random.choice">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">choice</code><span class="sig-paren">(</span><em class="sig-param">seq</em><span class="sig-paren">)</span><a class="headerlink" href="#random.choice" title="Permalink to this definition">¶</a></dt>
    <dd><p>Return a random element from the non-empty sequence <em>seq</em>. If <em>seq</em> is empty,
    raises <a class="reference internal" href="exceptions.html#IndexError" title="IndexError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">IndexError</span></code></a>.</p>
    </dd></dl>
    <dl class="function">
    <dt id="random.choices">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">choices</code><span class="sig-paren">(</span><em class="sig-param">population</em>, <em class="sig-param">weights=None</em>, <em class="sig-param">*</em>, <em class="sig-param">cum_weights=None</em>, <em class="sig-param">k=1</em><span class="sig-paren">)</span><a class="headerlink" href="#random.choices" title="Permalink to this definition">¶</a></dt>
    <dd><p>Return a <em>k</em> sized list of elements chosen from the <em>population</em> with replacement.
    If the <em>population</em> is empty, raises <a class="reference internal" href="exceptions.html#IndexError" title="IndexError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">IndexError</span></code></a>.</p>
    <p>If a <em>weights</em> sequence is specified, selections are made according to the
    relative weights.  Alternatively, if a <em>cum_weights</em> sequence is given, the
    selections are made according to the cumulative weights (perhaps computed
    using <a class="reference internal" href="itertools.html#itertools.accumulate" title="itertools.accumulate"><code class="xref py py-func docutils literal notranslate"><span class="pre">itertools.accumulate()</span></code></a>).  For example, the relative weights
    <code class="docutils literal notranslate"><span class="pre">[10,</span> <span class="pre">5,</span> <span class="pre">30,</span> <span class="pre">5]</span></code> are equivalent to the cumulative weights
    <code class="docutils literal notranslate"><span class="pre">[10,</span> <span class="pre">15,</span> <span class="pre">45,</span> <span class="pre">50]</span></code>.  Internally, the relative weights are converted to
    cumulative weights before making selections, so supplying the cumulative
    weights saves work.</p>
    <p>If neither <em>weights</em> nor <em>cum_weights</em> are specified, selections are made
    with equal probability.  If a weights sequence is supplied, it must be
    the same length as the <em>population</em> sequence.  It is a <a class="reference internal" href="exceptions.html#TypeError" title="TypeError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">TypeError</span></code></a>
    to specify both <em>weights</em> and <em>cum_weights</em>.</p>
    <p>The <em>weights</em> or <em>cum_weights</em> can use any numeric type that interoperates
    with the <a class="reference internal" href="functions.html#float" title="float"><code class="xref py py-class docutils literal notranslate"><span class="pre">float</span></code></a> values returned by <a class="reference internal" href="#module-random" title="random: Generate pseudo-random numbers with various common distributions."><code class="xref py py-func docutils literal notranslate"><span class="pre">random()</span></code></a> (that includes
    integers, floats, and fractions but excludes decimals).  Behavior is
    undefined if any weight is negative.  A <a class="reference internal" href="exceptions.html#ValueError" title="ValueError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">ValueError</span></code></a> is raised if all
    weights are zero.</p>
    <p>For a given seed, the <a class="reference internal" href="#random.choices" title="random.choices"><code class="xref py py-func docutils literal notranslate"><span class="pre">choices()</span></code></a> function with equal weighting
    typically produces a different sequence than repeated calls to
    <a class="reference internal" href="#random.choice" title="random.choice"><code class="xref py py-func docutils literal notranslate"><span class="pre">choice()</span></code></a>.  The algorithm used by <a class="reference internal" href="#random.choices" title="random.choices"><code class="xref py py-func docutils literal notranslate"><span class="pre">choices()</span></code></a> uses floating
    point arithmetic for internal consistency and speed.  The algorithm used
    by <a class="reference internal" href="#random.choice" title="random.choice"><code class="xref py py-func docutils literal notranslate"><span class="pre">choice()</span></code></a> defaults to integer arithmetic with repeated selections
    to avoid small biases from round-off error.</p>
    <div class="versionadded">
    <p><span class="versionmodified added">New in version 3.6.</span></p>
    </div>
    <div class="versionchanged">
    <p><span class="versionmodified changed">Changed in version 3.9: </span>Raises a <a class="reference internal" href="exceptions.html#ValueError" title="ValueError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">ValueError</span></code></a> if all weights are zero.</p>
    </div>
    </dd></dl>
    <dl class="function">
    <dt id="random.shuffle">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">shuffle</code><span class="sig-paren">(</span><em class="sig-param">x</em><span class="optional">[</span>, <em class="sig-param">random</em><span class="optional">]</span><span class="sig-paren">)</span><a class="headerlink" href="#random.shuffle" title="Permalink to this definition">¶</a></dt>
    <dd><p>Shuffle the sequence <em>x</em> in place.</p>
    <p>The optional argument <em>random</em> is a 0-argument function returning a random
    float in [0.0, 1.0); by default, this is the function <a class="reference internal" href="#random.random" title="random.random"><code class="xref py py-func docutils literal notranslate"><span class="pre">random()</span></code></a>.</p>
    <p>To shuffle an immutable sequence and return a new shuffled list, use
    <code class="docutils literal notranslate"><span class="pre">sample(x,</span> <span class="pre">k=len(x))</span></code> instead.</p>
    <p>Note that even for small <code class="docutils literal notranslate"><span class="pre">len(x)</span></code>, the total number of permutations of <em>x</em>
    can quickly grow larger than the period of most random number generators.
    This implies that most permutations of a long sequence can never be
    generated.  For example, a sequence of length 2080 is the largest that
    can fit within the period of the Mersenne Twister random number generator.</p>
    <div class="deprecated-removed">
    <p><span class="versionmodified">Deprecated since version 3.9, will be removed in version 3.11: </span>The optional parameter <em>random</em>.</p>
    </div>
    </dd></dl>
    <dl class="function">
    <dt id="random.sample">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">sample</code><span class="sig-paren">(</span><em class="sig-param">population</em>, <em class="sig-param">k</em>, <em class="sig-param">*</em>, <em class="sig-param">counts=None</em><span class="sig-paren">)</span><a class="headerlink" href="#random.sample" title="Permalink to this definition">¶</a></dt>
    <dd><p>Return a <em>k</em> length list of unique elements chosen from the population sequence
    or set. Used for random sampling without replacement.</p>
    <p>Returns a new list containing elements from the population while leaving the
    original population unchanged.  The resulting list is in selection order so that
    all sub-slices will also be valid random samples.  This allows raffle winners
    (the sample) to be partitioned into grand prize and second place winners (the
    subslices).</p>
    <p>Members of the population need not be <a class="reference internal" href="../glossary.html#term-hashable"><span class="xref std std-term">hashable</span></a> or unique.  If the population
    contains repeats, then each occurrence is a possible selection in the sample.</p>
    <p>Repeated elements can be specified one at a time or with the optional
    keyword-only <em>counts</em> parameter.  For example, <code class="docutils literal notranslate"><span class="pre">sample(['red',</span> <span class="pre">'blue'],</span>
    <span class="pre">counts=[4,</span> <span class="pre">2],</span> <span class="pre">k=5)</span></code> is equivalent to <code class="docutils literal notranslate"><span class="pre">sample(['red',</span> <span class="pre">'red',</span> <span class="pre">'red',</span> <span class="pre">'red',</span>
    <span class="pre">'blue',</span> <span class="pre">'blue'],</span> <span class="pre">k=5)</span></code>.</p>
    <p>To choose a sample from a range of integers, use a <a class="reference internal" href="stdtypes.html#range" title="range"><code class="xref py py-func docutils literal notranslate"><span class="pre">range()</span></code></a> object as an
    argument.  This is especially fast and space efficient for sampling from a large
    population:  <code class="docutils literal notranslate"><span class="pre">sample(range(10000000),</span> <span class="pre">k=60)</span></code>.</p>
    <p>If the sample size is larger than the population size, a <a class="reference internal" href="exceptions.html#ValueError" title="ValueError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">ValueError</span></code></a>
    is raised.</p>
    <div class="versionchanged">
    <p><span class="versionmodified changed">Changed in version 3.9: </span>Added the <em>counts</em> parameter.</p>
    </div>
    <div class="deprecated">
    <p><span class="versionmodified deprecated">Deprecated since version 3.9: </span>In the future, the <em>population</em> must be a sequence.  Instances of
    <a class="reference internal" href="stdtypes.html#set" title="set"><code class="xref py py-class docutils literal notranslate"><span class="pre">set</span></code></a> are no longer supported.  The set must first be converted
    to a <a class="reference internal" href="stdtypes.html#list" title="list"><code class="xref py py-class docutils literal notranslate"><span class="pre">list</span></code></a> or <a class="reference internal" href="stdtypes.html#tuple" title="tuple"><code class="xref py py-class docutils literal notranslate"><span class="pre">tuple</span></code></a>, preferably in a deterministic
    order so that the sample is reproducible.</p>
    </div>
    </dd></dl>
    </div>
    <div class="section" id="real-valued-distributions">
    <span id="id1"></span><h2>Real-valued distributions<a class="headerlink" href="#real-valued-distributions" title="Permalink to this headline">¶</a></h2>
    <p>The following functions generate specific real-valued distributions. Function
    parameters are named after the corresponding variables in the distribution’s
    equation, as used in common mathematical practice; most of these equations can
    be found in any statistics text.</p>
    <dl class="function">
    <dt id="random.random">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">random</code><span class="sig-paren">(</span><span class="sig-paren">)</span><a class="headerlink" href="#random.random" title="Permalink to this definition">¶</a></dt>
    <dd><p>Return the next random floating point number in the range [0.0, 1.0).</p>
    </dd></dl>
    <dl class="function">
    <dt id="random.uniform">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">uniform</code><span class="sig-paren">(</span><em class="sig-param">a</em>, <em class="sig-param">b</em><span class="sig-paren">)</span><a class="headerlink" href="#random.uniform" title="Permalink to this definition">¶</a></dt>
    <dd><p>Return a random floating point number <em>N</em> such that <code class="docutils literal notranslate"><span class="pre">a</span> <span class="pre">&lt;=</span> <span class="pre">N</span> <span class="pre">&lt;=</span> <span class="pre">b</span></code> for
    <code class="docutils literal notranslate"><span class="pre">a</span> <span class="pre">&lt;=</span> <span class="pre">b</span></code> and <code class="docutils literal notranslate"><span class="pre">b</span> <span class="pre">&lt;=</span> <span class="pre">N</span> <span class="pre">&lt;=</span> <span class="pre">a</span></code> for <code class="docutils literal notranslate"><span class="pre">b</span> <span class="pre">&lt;</span> <span class="pre">a</span></code>.</p>
    <p>The end-point value <code class="docutils literal notranslate"><span class="pre">b</span></code> may or may not be included in the range
    depending on floating-point rounding in the equation <code class="docutils literal notranslate"><span class="pre">a</span> <span class="pre">+</span> <span class="pre">(b-a)</span> <span class="pre">*</span> <span class="pre">random()</span></code>.</p>
    </dd></dl>
    <dl class="function">
    <dt id="random.triangular">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">triangular</code><span class="sig-paren">(</span><em class="sig-param">low</em>, <em class="sig-param">high</em>, <em class="sig-param">mode</em><span class="sig-paren">)</span><a class="headerlink" href="#random.triangular" title="Permalink to this definition">¶</a></dt>
    <dd><p>Return a random floating point number <em>N</em> such that <code class="docutils literal notranslate"><span class="pre">low</span> <span class="pre">&lt;=</span> <span class="pre">N</span> <span class="pre">&lt;=</span> <span class="pre">high</span></code> and
    with the specified <em>mode</em> between those bounds.  The <em>low</em> and <em>high</em> bounds
    default to zero and one.  The <em>mode</em> argument defaults to the midpoint
    between the bounds, giving a symmetric distribution.</p>
    </dd></dl>
    <dl class="function">
    <dt id="random.betavariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">betavariate</code><span class="sig-paren">(</span><em class="sig-param">alpha</em>, <em class="sig-param">beta</em><span class="sig-paren">)</span><a class="headerlink" href="#random.betavariate" title="Permalink to this definition">¶</a></dt>
    <dd><p>Beta distribution.  Conditions on the parameters are <code class="docutils literal notranslate"><span class="pre">alpha</span> <span class="pre">&gt;</span> <span class="pre">0</span></code> and
    <code class="docutils literal notranslate"><span class="pre">beta</span> <span class="pre">&gt;</span> <span class="pre">0</span></code>. Returned values range between 0 and 1.</p>
    </dd></dl>
    <dl class="function">
    <dt id="random.expovariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">expovariate</code><span class="sig-paren">(</span><em class="sig-param">lambd</em><span class="sig-paren">)</span><a class="headerlink" href="#random.expovariate" title="Permalink to this definition">¶</a></dt>
    <dd><p>Exponential distribution.  <em>lambd</em> is 1.0 divided by the desired
    mean.  It should be nonzero.  (The parameter would be called
    “lambda”, but that is a reserved word in Python.)  Returned values
    range from 0 to positive infinity if <em>lambd</em> is positive, and from
    negative infinity to 0 if <em>lambd</em> is negative.</p>
    </dd></dl>
    <dl class="function">
    <dt id="random.gammavariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">gammavariate</code><span class="sig-paren">(</span><em class="sig-param">alpha</em>, <em class="sig-param">beta</em><span class="sig-paren">)</span><a class="headerlink" href="#random.gammavariate" title="Permalink to this definition">¶</a></dt>
    <dd><p>Gamma distribution.  (<em>Not</em> the gamma function!)  Conditions on the
    parameters are <code class="docutils literal notranslate"><span class="pre">alpha</span> <span class="pre">&gt;</span> <span class="pre">0</span></code> and <code class="docutils literal notranslate"><span class="pre">beta</span> <span class="pre">&gt;</span> <span class="pre">0</span></code>.</p>
    <p>The probability distribution function is:</p>
    <div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span>          <span class="n">x</span> <span class="o">**</span> <span class="p">(</span><span class="n">alpha</span> <span class="o">-</span> <span class="mi">1</span><span class="p">)</span> <span class="o">*</span> <span class="n">math</span><span class="o">.</span><span class="n">exp</span><span class="p">(</span><span class="o">-</span><span class="n">x</span> <span class="o">/</span> <span class="n">beta</span><span class="p">)</span>
    <span class="n">pdf</span><span class="p">(</span><span class="n">x</span><span class="p">)</span> <span class="o">=</span>  <span class="o">--------------------------------------</span>
                <span class="n">math</span><span class="o">.</span><span class="n">gamma</span><span class="p">(</span><span class="n">alpha</span><span class="p">)</span> <span class="o">*</span> <span class="n">beta</span> <span class="o">**</span> <span class="n">alpha</span>
    </pre></div>
    </div>
    </dd></dl>
    <dl class="function">
    <dt id="random.gauss">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">gauss</code><span class="sig-paren">(</span><em class="sig-param">mu</em>, <em class="sig-param">sigma</em><span class="sig-paren">)</span><a class="headerlink" href="#random.gauss" title="Permalink to this definition">¶</a></dt>
    <dd><p>Gaussian distribution.  <em>mu</em> is the mean, and <em>sigma</em> is the standard
    deviation.  This is slightly faster than the <a class="reference internal" href="#random.normalvariate" title="random.normalvariate"><code class="xref py py-func docutils literal notranslate"><span class="pre">normalvariate()</span></code></a> function
    defined below.</p>
    <p>Multithreading note:  When two threads call this function
    simultaneously, it is possible that they will receive the
    same return value.  This can be avoided in three ways.
    1) Have each thread use a different instance of the random
    number generator. 2) Put locks around all calls. 3) Use the
    slower, but thread-safe <a class="reference internal" href="#random.normalvariate" title="random.normalvariate"><code class="xref py py-func docutils literal notranslate"><span class="pre">normalvariate()</span></code></a> function instead.</p>
    </dd></dl>
    <dl class="function">
    <dt id="random.lognormvariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">lognormvariate</code><span class="sig-paren">(</span><em class="sig-param">mu</em>, <em class="sig-param">sigma</em><span class="sig-paren">)</span><a class="headerlink" href="#random.lognormvariate" title="Permalink to this definition">¶</a></dt>
    <dd><p>Log normal distribution.  If you take the natural logarithm of this
    distribution, you’ll get a normal distribution with mean <em>mu</em> and standard
    deviation <em>sigma</em>.  <em>mu</em> can have any value, and <em>sigma</em> must be greater than
    zero.</p>
    </dd></dl>
    <dl class="function">
    <dt id="random.normalvariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">normalvariate</code><span class="sig-paren">(</span><em class="sig-param">mu</em>, <em class="sig-param">sigma</em><span class="sig-paren">)</span><a class="headerlink" href="#random.normalvariate" title="Permalink to this definition">¶</a></dt>
    <dd><p>Normal distribution.  <em>mu</em> is the mean, and <em>sigma</em> is the standard deviation.</p>
    </dd></dl>
    <dl class="function">
    <dt id="random.vonmisesvariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">vonmisesvariate</code><span class="sig-paren">(</span><em class="sig-param">mu</em>, <em class="sig-param">kappa</em><span class="sig-paren">)</span><a class="headerlink" href="#random.vonmisesvariate" title="Permalink to this definition">¶</a></dt>
    <dd><p><em>mu</em> is the mean angle, expressed in radians between 0 and 2*<em>pi</em>, and <em>kappa</em>
    is the concentration parameter, which must be greater than or equal to zero.  If
    <em>kappa</em> is equal to zero, this distribution reduces to a uniform random angle
    over the range 0 to 2*<em>pi</em>.</p>
    </dd></dl>
    <dl class="function">
    <dt id="random.paretovariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">paretovariate</code><span class="sig-paren">(</span><em class="sig-param">alpha</em><span class="sig-paren">)</span><a class="headerlink" href="#random.paretovariate" title="Permalink to this definition">¶</a></dt>
    <dd><p>Pareto distribution.  <em>alpha</em> is the shape parameter.</p>
    </dd></dl>
    <dl class="function">
    <dt id="random.weibullvariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">weibullvariate</code><span class="sig-paren">(</span><em class="sig-param">alpha</em>, <em class="sig-param">beta</em><span class="sig-paren">)</span><a class="headerlink" href="#random.weibullvariate" title="Permalink to this definition">¶</a></dt>
    <dd><p>Weibull distribution.  <em>alpha</em> is the scale parameter and <em>beta</em> is the shape
    parameter.</p>
    </dd></dl>
    </div>
    <div class="section" id="alternative-generator">
    <h2>Alternative Generator<a class="headerlink" href="#alternative-generator" title="Permalink to this headline">¶</a></h2>
    <dl class="class">
    <dt id="random.Random">
    <em class="property">class </em><code class="sig-prename descclassname">random.</code><code class="sig-name descname">Random</code><span class="sig-paren">(</span><span class="optional">[</span><em class="sig-param">seed</em><span class="optional">]</span><span class="sig-paren">)</span><a class="headerlink" href="#random.Random" title="Permalink to this definition">¶</a></dt>
    <dd><p>Class that implements the default pseudo-random number generator used by the
    <a class="reference internal" href="#module-random" title="random: Generate pseudo-random numbers with various common distributions."><code class="xref py py-mod docutils literal notranslate"><span class="pre">random</span></code></a> module.</p>
    <div class="deprecated">
    <p><span class="versionmodified deprecated">Deprecated since version 3.9: </span>In the future, the <em>seed</em> must be one of the following types:
    <code class="xref py py-class docutils literal notranslate"><span class="pre">NoneType</span></code>, <a class="reference internal" href="functions.html#int" title="int"><code class="xref py py-class docutils literal notranslate"><span class="pre">int</span></code></a>, <a class="reference internal" href="functions.html#float" title="float"><code class="xref py py-class docutils literal notranslate"><span class="pre">float</span></code></a>, <a class="reference internal" href="stdtypes.html#str" title="str"><code class="xref py py-class docutils literal notranslate"><span class="pre">str</span></code></a>,
    <a class="reference internal" href="stdtypes.html#bytes" title="bytes"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytes</span></code></a>, or <a class="reference internal" href="stdtypes.html#bytearray" title="bytearray"><code class="xref py py-class docutils literal notranslate"><span class="pre">bytearray</span></code></a>.</p>
    </div>
    </dd></dl>
    <dl class="class">
    <dt id="random.SystemRandom">
    <em class="property">class </em><code class="sig-prename descclassname">random.</code><code class="sig-name descname">SystemRandom</code><span class="sig-paren">(</span><span class="optional">[</span><em class="sig-param">seed</em><span class="optional">]</span><span class="sig-paren">)</span><a class="headerlink" href="#random.SystemRandom" title="Permalink to this definition">¶</a></dt>
    <dd><p>Class that uses the <a class="reference internal" href="os.html#os.urandom" title="os.urandom"><code class="xref py py-func docutils literal notranslate"><span class="pre">os.urandom()</span></code></a> function for generating random numbers
    from sources provided by the operating system. Not available on all systems.
    Does not rely on software state, and sequences are not reproducible. Accordingly,
    the <a class="reference internal" href="#random.seed" title="random.seed"><code class="xref py py-meth docutils literal notranslate"><span class="pre">seed()</span></code></a> method has no effect and is ignored.
    The <a class="reference internal" href="#random.getstate" title="random.getstate"><code class="xref py py-meth docutils literal notranslate"><span class="pre">getstate()</span></code></a> and <a class="reference internal" href="#random.setstate" title="random.setstate"><code class="xref py py-meth docutils literal notranslate"><span class="pre">setstate()</span></code></a> methods raise
    <a class="reference internal" href="exceptions.html#NotImplementedError" title="NotImplementedError"><code class="xref py py-exc docutils literal notranslate"><span class="pre">NotImplementedError</span></code></a> if called.</p>
    </dd></dl>
    </div>
    <div class="section" id="notes-on-reproducibility">
    <h2>Notes on Reproducibility<a class="headerlink" href="#notes-on-reproducibility" title="Permalink to this headline">¶</a></h2>
    <p>Sometimes it is useful to be able to reproduce the sequences given by a
    pseudo-random number generator.  By re-using a seed value, the same sequence should be
    reproducible from run to run as long as multiple threads are not running.</p>
    <p>Most of the random module’s algorithms and seeding functions are subject to
    change across Python versions, but two aspects are guaranteed not to change:</p>
    <ul class="simple">
    <li><p>If a new seeding method is added, then a backward compatible seeder will be
    offered.</p></li>
    <li><p>The generator’s <code class="xref py py-meth docutils literal notranslate"><span class="pre">random()</span></code> method will continue to produce the same
    sequence when the compatible seeder is given the same seed.</p></li>
    </ul>
    </div>
    <div class="section" id="examples">
    <span id="random-examples"></span><h2>Examples<a class="headerlink" href="#examples" title="Permalink to this headline">¶</a></h2>
    <p>Basic examples:</p>
    <div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="gp">&gt;&gt;&gt; </span><span class="n">random</span><span class="p">()</span>                             <span class="c1"># Random float:  0.0 &lt;= x &lt; 1.0</span>
    <span class="go">0.37444887175646646</span>
    
    <span class="gp">&gt;&gt;&gt; </span><span class="n">uniform</span><span class="p">(</span><span class="mf">2.5</span><span class="p">,</span> <span class="mf">10.0</span><span class="p">)</span>                   <span class="c1"># Random float:  2.5 &lt;= x &lt; 10.0</span>
    <span class="go">3.1800146073117523</span>
    
    <span class="gp">&gt;&gt;&gt; </span><span class="n">expovariate</span><span class="p">(</span><span class="mi">1</span> <span class="o">/</span> <span class="mi">5</span><span class="p">)</span>                   <span class="c1"># Interval between arrivals averaging 5 seconds</span>
    <span class="go">5.148957571865031</span>
    
    <span class="gp">&gt;&gt;&gt; </span><span class="n">randrange</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span>                        <span class="c1"># Integer from 0 to 9 inclusive</span>
    <span class="go">7</span>
    
    <span class="gp">&gt;&gt;&gt; </span><span class="n">randrange</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">101</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span>                 <span class="c1"># Even integer from 0 to 100 inclusive</span>
    <span class="go">26</span>
    
    <span class="gp">&gt;&gt;&gt; </span><span class="n">choice</span><span class="p">([</span><span class="s1">'win'</span><span class="p">,</span> <span class="s1">'lose'</span><span class="p">,</span> <span class="s1">'draw'</span><span class="p">])</span>      <span class="c1"># Single random element from a sequence</span>
    <span class="go">'draw'</span>
    
    <span class="gp">&gt;&gt;&gt; </span><span class="n">deck</span> <span class="o">=</span> <span class="s1">'ace two three four'</span><span class="o">.</span><span class="n">split</span><span class="p">()</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="n">shuffle</span><span class="p">(</span><span class="n">deck</span><span class="p">)</span>                        <span class="c1"># Shuffle a list</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="n">deck</span>
    <span class="go">['four', 'two', 'ace', 'three']</span>
    
    <span class="gp">&gt;&gt;&gt; </span><span class="n">sample</span><span class="p">([</span><span class="mi">10</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">30</span><span class="p">,</span> <span class="mi">40</span><span class="p">,</span> <span class="mi">50</span><span class="p">],</span> <span class="n">k</span><span class="o">=</span><span class="mi">4</span><span class="p">)</span>    <span class="c1"># Four samples without replacement</span>
    <span class="go">[40, 10, 50, 30]</span>
    </pre></div>
    </div>
    <p>Simulations:</p>
    <div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="gp">&gt;&gt;&gt; </span><span class="c1"># Six roulette wheel spins (weighted sampling with replacement)</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="n">choices</span><span class="p">([</span><span class="s1">'red'</span><span class="p">,</span> <span class="s1">'black'</span><span class="p">,</span> <span class="s1">'green'</span><span class="p">],</span> <span class="p">[</span><span class="mi">18</span><span class="p">,</span> <span class="mi">18</span><span class="p">,</span> <span class="mi">2</span><span class="p">],</span> <span class="n">k</span><span class="o">=</span><span class="mi">6</span><span class="p">)</span>
    <span class="go">['red', 'green', 'black', 'black', 'red', 'black']</span>
    
    <span class="gp">&gt;&gt;&gt; </span><span class="c1"># Deal 20 cards without replacement from a deck</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="c1"># of 52 playing cards, and determine the proportion of cards</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="c1"># with a ten-value:  ten, jack, queen, or king.</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="n">dealt</span> <span class="o">=</span> <span class="n">sample</span><span class="p">([</span><span class="s1">'tens'</span><span class="p">,</span> <span class="s1">'low cards'</span><span class="p">],</span> <span class="n">counts</span><span class="o">=</span><span class="p">[</span><span class="mi">16</span><span class="p">,</span> <span class="mi">36</span><span class="p">],</span> <span class="n">k</span><span class="o">=</span><span class="mi">20</span><span class="p">)</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="n">dealt</span><span class="o">.</span><span class="n">count</span><span class="p">(</span><span class="s1">'tens'</span><span class="p">)</span> <span class="o">/</span> <span class="mi">20</span>
    <span class="go">0.15</span>
    
    <span class="gp">&gt;&gt;&gt; </span><span class="c1"># Estimate the probability of getting 5 or more heads from 7 spins</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="c1"># of a biased coin that settles on heads 60% of the time.</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="k">def</span> <span class="nf">trial</span><span class="p">():</span>
    <span class="gp">... </span>    <span class="k">return</span> <span class="n">choices</span><span class="p">(</span><span class="s1">'HT'</span><span class="p">,</span> <span class="n">cum_weights</span><span class="o">=</span><span class="p">(</span><span class="mf">0.60</span><span class="p">,</span> <span class="mf">1.00</span><span class="p">),</span> <span class="n">k</span><span class="o">=</span><span class="mi">7</span><span class="p">)</span><span class="o">.</span><span class="n">count</span><span class="p">(</span><span class="s1">'H'</span><span class="p">)</span> <span class="o">&gt;=</span> <span class="mi">5</span>
    <span class="gp">...</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="nb">sum</span><span class="p">(</span><span class="n">trial</span><span class="p">()</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">10_000</span><span class="p">))</span> <span class="o">/</span> <span class="mi">10_000</span>
    <span class="go">0.4169</span>
    
    <span class="gp">&gt;&gt;&gt; </span><span class="c1"># Probability of the median of 5 samples being in middle two quartiles</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="k">def</span> <span class="nf">trial</span><span class="p">():</span>
    <span class="gp">... </span>    <span class="k">return</span> <span class="mi">2_500</span> <span class="o">&lt;=</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">choices</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="mi">10_000</span><span class="p">),</span> <span class="n">k</span><span class="o">=</span><span class="mi">5</span><span class="p">))[</span><span class="mi">2</span><span class="p">]</span> <span class="o">&lt;</span> <span class="mi">7_500</span>
    <span class="gp">...</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="nb">sum</span><span class="p">(</span><span class="n">trial</span><span class="p">()</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">10_000</span><span class="p">))</span> <span class="o">/</span> <span class="mi">10_000</span>
    <span class="go">0.7958</span>
    </pre></div>
    </div>
    <p>Example of <a class="reference external" href="https://en.wikipedia.org/wiki/Bootstrapping_(statistics)">statistical bootstrapping</a> using resampling
    with replacement to estimate a confidence interval for the mean of a sample:</p>
    <div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="c1"># http://statistics.about.com/od/Applications/a/Example-Of-Bootstrapping.htm</span>
    <span class="kn">from</span> <span class="nn">statistics</span> <span class="kn">import</span> <span class="n">fmean</span> <span class="k">as</span> <span class="n">mean</span>
    <span class="kn">from</span> <span class="nn">random</span> <span class="kn">import</span> <span class="n">choices</span>
    
    <span class="n">data</span> <span class="o">=</span> <span class="p">[</span><span class="mi">41</span><span class="p">,</span> <span class="mi">50</span><span class="p">,</span> <span class="mi">29</span><span class="p">,</span> <span class="mi">37</span><span class="p">,</span> <span class="mi">81</span><span class="p">,</span> <span class="mi">30</span><span class="p">,</span> <span class="mi">73</span><span class="p">,</span> <span class="mi">63</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">35</span><span class="p">,</span> <span class="mi">68</span><span class="p">,</span> <span class="mi">22</span><span class="p">,</span> <span class="mi">60</span><span class="p">,</span> <span class="mi">31</span><span class="p">,</span> <span class="mi">95</span><span class="p">]</span>
    <span class="n">means</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">mean</span><span class="p">(</span><span class="n">choices</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">k</span><span class="o">=</span><span class="nb">len</span><span class="p">(</span><span class="n">data</span><span class="p">)))</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">100</span><span class="p">))</span>
    <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">'The sample mean of </span><span class="si">{</span><span class="n">mean</span><span class="p">(</span><span class="n">data</span><span class="p">)</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1"> has a 90% confidence '</span>
          <span class="sa">f</span><span class="s1">'interval from </span><span class="si">{</span><span class="n">means</span><span class="p">[</span><span class="mi">5</span><span class="p">]</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1"> to </span><span class="si">{</span><span class="n">means</span><span class="p">[</span><span class="mi">94</span><span class="p">]</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1">'</span><span class="p">)</span>
    </pre></div>
    </div>
    <p>Example of a <a class="reference external" href="https://en.wikipedia.org/wiki/Resampling_(statistics)#Permutation_tests">resampling permutation test</a>
    to determine the statistical significance or <a class="reference external" href="https://en.wikipedia.org/wiki/P-value">p-value</a> of an observed difference
    between the effects of a drug versus a placebo:</p>
    <div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="c1"># Example from "Statistics is Easy" by Dennis Shasha and Manda Wilson</span>
    <span class="kn">from</span> <span class="nn">statistics</span> <span class="kn">import</span> <span class="n">fmean</span> <span class="k">as</span> <span class="n">mean</span>
    <span class="kn">from</span> <span class="nn">random</span> <span class="kn">import</span> <span class="n">shuffle</span>
    
    <span class="n">drug</span> <span class="o">=</span> <span class="p">[</span><span class="mi">54</span><span class="p">,</span> <span class="mi">73</span><span class="p">,</span> <span class="mi">53</span><span class="p">,</span> <span class="mi">70</span><span class="p">,</span> <span class="mi">73</span><span class="p">,</span> <span class="mi">68</span><span class="p">,</span> <span class="mi">52</span><span class="p">,</span> <span class="mi">65</span><span class="p">,</span> <span class="mi">65</span><span class="p">]</span>
    <span class="n">placebo</span> <span class="o">=</span> <span class="p">[</span><span class="mi">54</span><span class="p">,</span> <span class="mi">51</span><span class="p">,</span> <span class="mi">58</span><span class="p">,</span> <span class="mi">44</span><span class="p">,</span> <span class="mi">55</span><span class="p">,</span> <span class="mi">52</span><span class="p">,</span> <span class="mi">42</span><span class="p">,</span> <span class="mi">47</span><span class="p">,</span> <span class="mi">58</span><span class="p">,</span> <span class="mi">46</span><span class="p">]</span>
    <span class="n">observed_diff</span> <span class="o">=</span> <span class="n">mean</span><span class="p">(</span><span class="n">drug</span><span class="p">)</span> <span class="o">-</span> <span class="n">mean</span><span class="p">(</span><span class="n">placebo</span><span class="p">)</span>
    
    <span class="n">n</span> <span class="o">=</span> <span class="mi">10_000</span>
    <span class="n">count</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="n">combined</span> <span class="o">=</span> <span class="n">drug</span> <span class="o">+</span> <span class="n">placebo</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n</span><span class="p">):</span>
        <span class="n">shuffle</span><span class="p">(</span><span class="n">combined</span><span class="p">)</span>
        <span class="n">new_diff</span> <span class="o">=</span> <span class="n">mean</span><span class="p">(</span><span class="n">combined</span><span class="p">[:</span><span class="nb">len</span><span class="p">(</span><span class="n">drug</span><span class="p">)])</span> <span class="o">-</span> <span class="n">mean</span><span class="p">(</span><span class="n">combined</span><span class="p">[</span><span class="nb">len</span><span class="p">(</span><span class="n">drug</span><span class="p">):])</span>
        <span class="n">count</span> <span class="o">+=</span> <span class="p">(</span><span class="n">new_diff</span> <span class="o">&gt;=</span> <span class="n">observed_diff</span><span class="p">)</span>
    
    <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">'</span><span class="si">{</span><span class="n">n</span><span class="si">}</span><span class="s1"> label reshufflings produced only </span><span class="si">{</span><span class="n">count</span><span class="si">}</span><span class="s1"> instances with a difference'</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">'at least as extreme as the observed difference of </span><span class="si">{</span><span class="n">observed_diff</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1">.'</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">'The one-sided p-value of </span><span class="si">{</span><span class="n">count</span> <span class="o">/</span> <span class="n">n</span><span class="si">:</span><span class="s1">.4f</span><span class="si">}</span><span class="s1"> leads us to reject the null'</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">'hypothesis that there is no difference between the drug and the placebo.'</span><span class="p">)</span>
    </pre></div>
    </div>
    <p>Simulation of arrival times and service deliveries for a multiserver queue:</p>
    <div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="kn">from</span> <span class="nn">heapq</span> <span class="kn">import</span> <span class="n">heappush</span><span class="p">,</span> <span class="n">heappop</span>
    <span class="kn">from</span> <span class="nn">random</span> <span class="kn">import</span> <span class="n">expovariate</span><span class="p">,</span> <span class="n">gauss</span>
    <span class="kn">from</span> <span class="nn">statistics</span> <span class="kn">import</span> <span class="n">mean</span><span class="p">,</span> <span class="n">median</span><span class="p">,</span> <span class="n">stdev</span>
    
    <span class="n">average_arrival_interval</span> <span class="o">=</span> <span class="mf">5.6</span>
    <span class="n">average_service_time</span> <span class="o">=</span> <span class="mf">15.0</span>
    <span class="n">stdev_service_time</span> <span class="o">=</span> <span class="mf">3.5</span>
    <span class="n">num_servers</span> <span class="o">=</span> <span class="mi">3</span>
    
    <span class="n">waits</span> <span class="o">=</span> <span class="p">[]</span>
    <span class="n">arrival_time</span> <span class="o">=</span> <span class="mf">0.0</span>
    <span class="n">servers</span> <span class="o">=</span> <span class="p">[</span><span class="mf">0.0</span><span class="p">]</span> <span class="o">*</span> <span class="n">num_servers</span>  <span class="c1"># time when each server becomes available</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">100_000</span><span class="p">):</span>
        <span class="n">arrival_time</span> <span class="o">+=</span> <span class="n">expovariate</span><span class="p">(</span><span class="mf">1.0</span> <span class="o">/</span> <span class="n">average_arrival_interval</span><span class="p">)</span>
        <span class="n">next_server_available</span> <span class="o">=</span> <span class="n">heappop</span><span class="p">(</span><span class="n">servers</span><span class="p">)</span>
        <span class="n">wait</span> <span class="o">=</span> <span class="nb">max</span><span class="p">(</span><span class="mf">0.0</span><span class="p">,</span> <span class="n">next_server_available</span> <span class="o">-</span> <span class="n">arrival_time</span><span class="p">)</span>
        <span class="n">waits</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">wait</span><span class="p">)</span>
        <span class="n">service_duration</span> <span class="o">=</span> <span class="n">gauss</span><span class="p">(</span><span class="n">average_service_time</span><span class="p">,</span> <span class="n">stdev_service_time</span><span class="p">)</span>
        <span class="n">service_completed</span> <span class="o">=</span> <span class="n">arrival_time</span> <span class="o">+</span> <span class="n">wait</span> <span class="o">+</span> <span class="n">service_duration</span>
        <span class="n">heappush</span><span class="p">(</span><span class="n">servers</span><span class="p">,</span> <span class="n">service_completed</span><span class="p">)</span>
    
    <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">'Mean wait: </span><span class="si">{</span><span class="n">mean</span><span class="p">(</span><span class="n">waits</span><span class="p">)</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1">.  Stdev wait: </span><span class="si">{</span><span class="n">stdev</span><span class="p">(</span><span class="n">waits</span><span class="p">)</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1">.'</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s1">'Median wait: </span><span class="si">{</span><span class="n">median</span><span class="p">(</span><span class="n">waits</span><span class="p">)</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1">.  Max wait: </span><span class="si">{</span><span class="nb">max</span><span class="p">(</span><span class="n">waits</span><span class="p">)</span><span class="si">:</span><span class="s1">.1f</span><span class="si">}</span><span class="s1">.'</span><span class="p">)</span>
    </pre></div>
    </div>
    <div class="admonition seealso">
    <p class="admonition-title">See also</p>
    <p><a class="reference external" href="https://www.youtube.com/watch?v=Iq9DzN6mvYA">Statistics for Hackers</a>
    a video tutorial by
    <a class="reference external" href="https://us.pycon.org/2016/speaker/profile/295/">Jake Vanderplas</a>
    on statistical analysis using just a few fundamental concepts
    including simulation, sampling, shuffling, and cross-validation.</p>
    <p><a class="reference external" href="http://nbviewer.jupyter.org/url/norvig.com/ipython/Economics.ipynb">Economics Simulation</a>
    a simulation of a marketplace by
    <a class="reference external" href="http://norvig.com/bio.html">Peter Norvig</a> that shows effective
    use of many of the tools and distributions provided by this module
    (gauss, uniform, sample, betavariate, choice, triangular, and randrange).</p>
    <p><a class="reference external" href="http://nbviewer.jupyter.org/url/norvig.com/ipython/Probability.ipynb">A Concrete Introduction to Probability (using Python)</a>
    a tutorial by <a class="reference external" href="http://norvig.com/bio.html">Peter Norvig</a> covering
    the basics of probability theory, how to write simulations, and
    how to perform data analysis using Python.</p>
    </div>
    </div>
    <div class="section" id="recipes">
    <h2>Recipes<a class="headerlink" href="#recipes" title="Permalink to this headline">¶</a></h2>
    <p>The default <a class="reference internal" href="#random.random" title="random.random"><code class="xref py py-func docutils literal notranslate"><span class="pre">random()</span></code></a> returns multiples of 2⁻⁵³ in the range
    <em>0.0 ≤ x &lt; 1.0</em>.  All such numbers are evenly spaced and are exactly
    representable as Python floats.  However, many other representable
    floats in that interval are not possible selections.  For example,
    <code class="docutils literal notranslate"><span class="pre">0.05954861408025609</span></code> isn’t an integer multiple of 2⁻⁵³.</p>
    <p>The following recipe takes a different approach.  All floats in the
    interval are possible selections.  The mantissa comes from a uniform
    distribution of integers in the range <em>2⁵² ≤ mantissa &lt; 2⁵³</em>.  The
    exponent comes from a geometric distribution where exponents smaller
    than <em>-53</em> occur half as often as the next larger exponent.</p>
    <div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="kn">from</span> <span class="nn">random</span> <span class="kn">import</span> <span class="n">Random</span>
    <span class="kn">from</span> <span class="nn">math</span> <span class="kn">import</span> <span class="n">ldexp</span>
    
    <span class="k">class</span> <span class="nc">FullRandom</span><span class="p">(</span><span class="n">Random</span><span class="p">):</span>
    
        <span class="k">def</span> <span class="nf">random</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
            <span class="n">mantissa</span> <span class="o">=</span> <span class="mh">0x10_0000_0000_0000</span> <span class="o">|</span> <span class="bp">self</span><span class="o">.</span><span class="n">getrandbits</span><span class="p">(</span><span class="mi">52</span><span class="p">)</span>
            <span class="n">exponent</span> <span class="o">=</span> <span class="o">-</span><span class="mi">53</span>
            <span class="n">x</span> <span class="o">=</span> <span class="mi">0</span>
            <span class="k">while</span> <span class="ow">not</span> <span class="n">x</span><span class="p">:</span>
                <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">getrandbits</span><span class="p">(</span><span class="mi">32</span><span class="p">)</span>
                <span class="n">exponent</span> <span class="o">+=</span> <span class="n">x</span><span class="o">.</span><span class="n">bit_length</span><span class="p">()</span> <span class="o">-</span> <span class="mi">32</span>
            <span class="k">return</span> <span class="n">ldexp</span><span class="p">(</span><span class="n">mantissa</span><span class="p">,</span> <span class="n">exponent</span><span class="p">)</span>
    </pre></div>
    </div>
    <p>All <a class="reference internal" href="#real-valued-distributions"><span class="std std-ref">real valued distributions</span></a>
    in the class will use the new method:</p>
    <div class="highlight-python3 notranslate"><div class="highlight"><pre><span></span><span class="gp">&gt;&gt;&gt; </span><span class="n">fr</span> <span class="o">=</span> <span class="n">FullRandom</span><span class="p">()</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="n">fr</span><span class="o">.</span><span class="n">random</span><span class="p">()</span>
    <span class="go">0.05954861408025609</span>
    <span class="gp">&gt;&gt;&gt; </span><span class="n">fr</span><span class="o">.</span><span class="n">expovariate</span><span class="p">(</span><span class="mf">0.25</span><span class="p">)</span>
    <span class="go">8.87925541791544</span>
    </pre></div>
    </div>
    <p>The recipe is conceptually equivalent to an algorithm that chooses from
    all the multiples of 2⁻¹⁰⁷⁴ in the range <em>0.0 ≤ x &lt; 1.0</em>.  All such
    numbers are evenly spaced, but most have to be rounded down to the
    nearest representable Python float.  (The value 2⁻¹⁰⁷⁴ is the smallest
    positive unnormalized float and is equal to <code class="docutils literal notranslate"><span class="pre">math.ulp(0.0)</span></code>.)</p>
    <div class="admonition seealso">
    <p class="admonition-title">See also</p>
    <p><a class="reference external" href="https://allendowney.com/research/rand/downey07randfloat.pdf">Generating Pseudo-random Floating-Point Values</a> a
    paper by Allen B. Downey describing ways to generate more
    fine-grained floats than normally generated by <a class="reference internal" href="#random.random" title="random.random"><code class="xref py py-func docutils literal notranslate"><span class="pre">random()</span></code></a>.</p>
    </div>
    </div>
    </div>
    </div>
    </div>
    </div>
    <div aria-label="main navigation" class="sphinxsidebar" role="navigation">
    <div class="sphinxsidebarwrapper">
    <h3><a href="../contents.html">Table of Contents</a></h3>
    <ul>
    <li><a class="reference internal" href="#"><code class="xref py py-mod docutils literal notranslate"><span class="pre">random</span></code> — Generate pseudo-random numbers</a><ul>
    <li><a class="reference internal" href="#bookkeeping-functions">Bookkeeping functions</a></li>
    <li><a class="reference internal" href="#functions-for-bytes">Functions for bytes</a></li>
    <li><a class="reference internal" href="#functions-for-integers">Functions for integers</a></li>
    <li><a class="reference internal" href="#functions-for-sequences">Functions for sequences</a></li>
    <li><a class="reference internal" href="#real-valued-distributions">Real-valued distributions</a></li>
    <li><a class="reference internal" href="#alternative-generator">Alternative Generator</a></li>
    <li><a class="reference internal" href="#notes-on-reproducibility">Notes on Reproducibility</a></li>
    <li><a class="reference internal" href="#examples">Examples</a></li>
    <li><a class="reference internal" href="#recipes">Recipes</a></li>
    </ul>
    </li>
    </ul>
    <h4>Previous topic</h4>
    <p class="topless"><a href="fractions.html" title="previous chapter"><code class="xref py py-mod docutils literal notranslate"><span class="pre">fractions</span></code> — Rational numbers</a></p>
    <h4>Next topic</h4>
    <p class="topless"><a href="statistics.html" title="next chapter"><code class="xref py py-mod docutils literal notranslate"><span class="pre">statistics</span></code> — Mathematical statistics functions</a></p>
    <div aria-label="source link" role="note">
    <h3>This Page</h3>
    <ul class="this-page-menu">
    <li><a href="../bugs.html">Report a Bug</a></li>
    <li>
    <a href="https://github.com/python/cpython/blob/master/Doc/library/random.rst" rel="nofollow">Show Source
            </a>
    </li>
    </ul>
    </div>
    </div>
    </div>
    <div class="clearer"></div>
    </div>
    <div aria-label="related navigation" class="related" role="navigation">
    <h3>Navigation</h3>
    <ul>
    <li class="right" style="margin-right: 10px">
    <a href="../genindex.html" title="General Index">index</a></li>
    <li class="right">
    <a href="../py-modindex.html" title="Python Module Index">modules</a> |</li>
    <li class="right">
    <a href="statistics.html" title="statistics — Mathematical statistics functions">next</a> |</li>
    <li class="right">
    <a href="fractions.html" title="fractions — Rational numbers">previous</a> |</li>
    <li><img alt="" src="../_static/py.png" style="vertical-align: middle; margin-top: -1px"/></li>
    <li><a href="https://www.python.org/">Python</a> »</li>
    <li>
    <a href="../index.html">3.9.2 Documentation</a> »
        </li>
    <li class="nav-item nav-item-1"><a href="index.html">The Python Standard Library</a> »</li>
    <li class="nav-item nav-item-2"><a href="numeric.html">Numeric and Mathematical Modules</a> »</li>
    <li class="right">
    <div class="inline-search" role="search" style="display: none">
    <form action="../search.html" class="inline-search" method="get">
    <input name="q" placeholder="Quick search" type="text"/>
    <input type="submit" value="Go"/>
    <input name="check_keywords" type="hidden" value="yes"/>
    <input name="area" type="hidden" value="default"/>
    </form>
    </div>
    <script type="text/javascript">$('.inline-search').show(0);</script>
             |
        </li>
    </ul>
    </div>
    <div class="footer">
        © <a href="../copyright.html">Copyright</a> 2001-2021, Python Software Foundation.
        <br/>
    
        The Python Software Foundation is a non-profit corporation.
    <a href="https://www.python.org/psf/donations/">Please donate.</a>
    <br/>
    <br/>
    
        Last updated on Mar 24, 2021.
        <a href="https://docs.python.org/3/bugs.html">Found a bug</a>?
        <br/>
    
        Created using <a href="https://www.sphinx-doc.org/">Sphinx</a> 2.4.4.
=======
          Created using <a href="https://www.sphinx-doc.org/">Sphinx</a> 2.4.4.
>>>>>>> First commit
        </div>
    <script src="../_static/switchers.js" type="text/javascript"></script>
    </body>
    </html>




```python
# Other way to load the html code using 'urllib.request.urlopen()'

#url = urllib.request.urlopen("https://docs.python.org/3/library/random.html#module-random")
#soup = BeautifulSoup(url)
#soup
```

**Still very long, but a little easier to take in.**

The real advantage of Beautiful Soup, however, is that it *parses* our webpage according to its structure and allows us to *search for* and *extract* elements within it. This is because it transforms the webpage from a string into a special Beautiful Soup object.

To extract HTML elements from our webpage, we can call the `.find()` method on our Beautiful Soup object. This method finds the first element that matches the criterion that we pass in. The criterion may be an element `id`, `class`, tag `name`, or even a function. (For a full list of search elements, see [this page](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#searching-the-tree).)

But how do we know what element to search for? This is where your browser's `Inspect` or `Inspect Element` feature comes in handy. Simply right click on an object of interest on the web page and click `Inspect` on Chrome or `Inspect Element` on Firefox. This will then show you the corresponding place in the HTML code where the element appears. From there you should be able to find an id or class name that will allow you to locate the element with Beautiful Soup.

**In this case, we want to target the tag/ element `dt` as below picture:**

<br>
<br>
<img src = "https://docs.google.com/uc?export=download&id=1Mj9K4QnhS5mFMK4Ddx_6OHFUIN-xpR9X" />

<br>
<br>

**So it looks like we're looking for a `dt` element with `id='random.___'`. We can easily retrieve this with Beautiful Soup's `.findAll` command.**


```python
# Find all function names - we specify the name of the element in this case is 'dt'

names = soup.body.findAll('dt')

print(names)
```

    [<dt id="random.seed">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">seed</code><span class="sig-paren">(</span><em class="sig-param">a=None</em>, <em class="sig-param">version=2</em><span class="sig-paren">)</span><a class="headerlink" href="#random.seed" title="Permalink to this definition">¶</a></dt>, <dt id="random.getstate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">getstate</code><span class="sig-paren">(</span><span class="sig-paren">)</span><a class="headerlink" href="#random.getstate" title="Permalink to this definition">¶</a></dt>, <dt id="random.setstate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">setstate</code><span class="sig-paren">(</span><em class="sig-param">state</em><span class="sig-paren">)</span><a class="headerlink" href="#random.setstate" title="Permalink to this definition">¶</a></dt>, <dt id="random.randbytes">
<<<<<<< HEAD
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">randbytes</code><span class="sig-paren">(</span><em class="sig-param">n</em><span class="sig-paren">)</span><a class="headerlink" href="#random.randbytes" title="Permalink to this definition">¶</a></dt>, <dt id="random.randrange">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">randrange</code><span class="sig-paren">(</span><em class="sig-param">stop</em><span class="sig-paren">)</span><a class="headerlink" href="#random.randrange" title="Permalink to this definition">¶</a></dt>, <dt>
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">randrange</code><span class="sig-paren">(</span><em class="sig-param">start</em>, <em class="sig-param">stop</em><span class="optional">[</span>, <em class="sig-param">step</em><span class="optional">]</span><span class="sig-paren">)</span></dt>, <dt id="random.randint">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">randint</code><span class="sig-paren">(</span><em class="sig-param">a</em>, <em class="sig-param">b</em><span class="sig-paren">)</span><a class="headerlink" href="#random.randint" title="Permalink to this definition">¶</a></dt>, <dt id="random.getrandbits">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">getrandbits</code><span class="sig-paren">(</span><em class="sig-param">k</em><span class="sig-paren">)</span><a class="headerlink" href="#random.getrandbits" title="Permalink to this definition">¶</a></dt>, <dt id="random.choice">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">choice</code><span class="sig-paren">(</span><em class="sig-param">seq</em><span class="sig-paren">)</span><a class="headerlink" href="#random.choice" title="Permalink to this definition">¶</a></dt>, <dt id="random.choices">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">choices</code><span class="sig-paren">(</span><em class="sig-param">population</em>, <em class="sig-param">weights=None</em>, <em class="sig-param">*</em>, <em class="sig-param">cum_weights=None</em>, <em class="sig-param">k=1</em><span class="sig-paren">)</span><a class="headerlink" href="#random.choices" title="Permalink to this definition">¶</a></dt>, <dt id="random.shuffle">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">shuffle</code><span class="sig-paren">(</span><em class="sig-param">x</em><span class="optional">[</span>, <em class="sig-param">random</em><span class="optional">]</span><span class="sig-paren">)</span><a class="headerlink" href="#random.shuffle" title="Permalink to this definition">¶</a></dt>, <dt id="random.sample">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">sample</code><span class="sig-paren">(</span><em class="sig-param">population</em>, <em class="sig-param">k</em>, <em class="sig-param">*</em>, <em class="sig-param">counts=None</em><span class="sig-paren">)</span><a class="headerlink" href="#random.sample" title="Permalink to this definition">¶</a></dt>, <dt id="random.random">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">random</code><span class="sig-paren">(</span><span class="sig-paren">)</span><a class="headerlink" href="#random.random" title="Permalink to this definition">¶</a></dt>, <dt id="random.uniform">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">uniform</code><span class="sig-paren">(</span><em class="sig-param">a</em>, <em class="sig-param">b</em><span class="sig-paren">)</span><a class="headerlink" href="#random.uniform" title="Permalink to this definition">¶</a></dt>, <dt id="random.triangular">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">triangular</code><span class="sig-paren">(</span><em class="sig-param">low</em>, <em class="sig-param">high</em>, <em class="sig-param">mode</em><span class="sig-paren">)</span><a class="headerlink" href="#random.triangular" title="Permalink to this definition">¶</a></dt>, <dt id="random.betavariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">betavariate</code><span class="sig-paren">(</span><em class="sig-param">alpha</em>, <em class="sig-param">beta</em><span class="sig-paren">)</span><a class="headerlink" href="#random.betavariate" title="Permalink to this definition">¶</a></dt>, <dt id="random.expovariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">expovariate</code><span class="sig-paren">(</span><em class="sig-param">lambd</em><span class="sig-paren">)</span><a class="headerlink" href="#random.expovariate" title="Permalink to this definition">¶</a></dt>, <dt id="random.gammavariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">gammavariate</code><span class="sig-paren">(</span><em class="sig-param">alpha</em>, <em class="sig-param">beta</em><span class="sig-paren">)</span><a class="headerlink" href="#random.gammavariate" title="Permalink to this definition">¶</a></dt>, <dt id="random.gauss">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">gauss</code><span class="sig-paren">(</span><em class="sig-param">mu</em>, <em class="sig-param">sigma</em><span class="sig-paren">)</span><a class="headerlink" href="#random.gauss" title="Permalink to this definition">¶</a></dt>, <dt id="random.lognormvariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">lognormvariate</code><span class="sig-paren">(</span><em class="sig-param">mu</em>, <em class="sig-param">sigma</em><span class="sig-paren">)</span><a class="headerlink" href="#random.lognormvariate" title="Permalink to this definition">¶</a></dt>, <dt id="random.normalvariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">normalvariate</code><span class="sig-paren">(</span><em class="sig-param">mu</em>, <em class="sig-param">sigma</em><span class="sig-paren">)</span><a class="headerlink" href="#random.normalvariate" title="Permalink to this definition">¶</a></dt>, <dt id="random.vonmisesvariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">vonmisesvariate</code><span class="sig-paren">(</span><em class="sig-param">mu</em>, <em class="sig-param">kappa</em><span class="sig-paren">)</span><a class="headerlink" href="#random.vonmisesvariate" title="Permalink to this definition">¶</a></dt>, <dt id="random.paretovariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">paretovariate</code><span class="sig-paren">(</span><em class="sig-param">alpha</em><span class="sig-paren">)</span><a class="headerlink" href="#random.paretovariate" title="Permalink to this definition">¶</a></dt>, <dt id="random.weibullvariate">
    <code class="sig-prename descclassname">random.</code><code class="sig-name descname">weibullvariate</code><span class="sig-paren">(</span><em class="sig-param">alpha</em>, <em class="sig-param">beta</em><span class="sig-paren">)</span><a class="headerlink" href="#random.weibullvariate" title="Permalink to this definition">¶</a></dt>, <dt id="random.Random">
    <em class="property">class </em><code class="sig-prename descclassname">random.</code><code class="sig-name descname">Random</code><span class="sig-paren">(</span><span class="optional">[</span><em class="sig-param">seed</em><span class="optional">]</span><span class="sig-paren">)</span><a class="headerlink" href="#random.Random" title="Permalink to this definition">¶</a></dt>, <dt id="random.SystemRandom">
    <em class="property">class </em><code class="sig-prename descclassname">random.</code><code class="sig-name descname">SystemRandom</code><span class="sig-paren">(</span><span class="optional">[</span><em class="sig-param">seed</em><span class="optional">]</span><span class="sig-paren">)</span><a class="headerlink" href="#random.SystemRandom" title="Permalink to this definition">¶</a></dt>]


**There are still some works to do! This is when regex kicks in.**



```python
# Find all the information we're looking for with regex
# In this case, it would be every string at starts with id='random.'

function_names = re.findall('id="random.\w+' , str(names)) # '\w+' which means the string should end with the function name

# Let print the results
print(function_names)
```

    ['id="random.seed', 'id="random.getstate', 'id="random.setstate', 'id="random.randbytes', 'id="random.randrange', 'id="random.randint', 'id="random.getrandbits', 'id="random.choice', 'id="random.choices', 'id="random.shuffle', 'id="random.sample', 'id="random.random', 'id="random.uniform', 'id="random.triangular', 'id="random.betavariate', 'id="random.expovariate', 'id="random.gammavariate', 'id="random.gauss', 'id="random.lognormvariate', 'id="random.normalvariate', 'id="random.vonmisesvariate', 'id="random.paretovariate', 'id="random.weibullvariate', 'id="random.Random', 'id="random.SystemRandom']


**We are almost there! We just need to remove the first few characters from each string.**


```python
# Using list comprehension to edit our values:

function_names = [item[4:] for item in function_names]

# Let print the results
print(function_names)
```

    ['random.seed', 'random.getstate', 'random.setstate', 'random.randbytes', 'random.randrange', 'random.randint', 'random.getrandbits', 'random.choice', 'random.choices', 'random.shuffle', 'random.sample', 'random.random', 'random.uniform', 'random.triangular', 'random.betavariate', 'random.expovariate', 'random.gammavariate', 'random.gauss', 'random.lognormvariate', 'random.normalvariate', 'random.vonmisesvariate', 'random.paretovariate', 'random.weibullvariate', 'random.Random', 'random.SystemRandom']


**Perfect! Now we need to do the same with the function description.
We have to target the description details with tag - `dd`**

<br>


<img src = "https://docs.google.com/uc?export=download&id=169-W93jfnmbwHejyP4QV4sDQm9LgriwB" />

<br>
<br>


```python
# Find all the function description

description = soup.body.findAll('dd')

#print(description)
```

**Wow it looks very complicated! There are lots of tags here (`<em>` tags). These unnecessary elements from the above method would take a long time to get rid of manually.**
    
Luckily, BeautifulSoup is not only beautiful, it's also smart. Let's look at the `.text` method:


```python
# Create a list

function_usage = []

# Create a loop

for item in description:
    item = item.text      #  Save the extracted text to a variable
    item = item.replace('\n', ' ')     # to get rid of the next line operator which is `\n` 
    function_usage.append(item)
    
#print(function_usage)  # Don't get overwhelmed! they are just all the function description from the above function names
```


```python
# Let's check the length of the function_names and function_usage

print(f' Length of function_names: {len(function_names)}')
print(f' Length of function_usage: {len(function_usage)}')
```

     Length of function_names: 25
     Length of function_usage: 25


### Make A Database


```python
# Create a dataframe since the length of both variables are equal!

data = pd.DataFrame( {  'function name': function_names, 
                      'function usage' : function_usage  } )

data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>function name</th>
      <th>function usage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>random.seed</td>
      <td>Initialize the random number generator.If a is...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>random.getstate</td>
      <td>Return an object capturing the current interna...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>random.setstate</td>
      <td>state should have been obtained from a previou...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>random.randbytes</td>
      <td>Generate n random bytes.This method should not...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>random.randrange</td>
      <td>Return a randomly selected element from range(...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>random.randint</td>
      <td>Return a random integer N such that a &lt;= N &lt;= ...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>random.getrandbits</td>
      <td>Returns a non-negative Python integer with k r...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>random.choice</td>
      <td>Return a random element from the non-empty seq...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>random.choices</td>
      <td>Return a k sized list of elements chosen from ...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>random.shuffle</td>
      <td>Shuffle the sequence x in place.The optional a...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>random.sample</td>
      <td>Return a k length list of unique elements chos...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>random.random</td>
      <td>Return the next random floating point number i...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>random.uniform</td>
      <td>Return a random floating point number N such t...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>random.triangular</td>
      <td>Return a random floating point number N such t...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>random.betavariate</td>
      <td>Beta distribution.  Conditions on the paramete...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>random.expovariate</td>
      <td>Exponential distribution.  lambd is 1.0 divide...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>random.gammavariate</td>
      <td>Gamma distribution.  (Not the gamma function!)...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>random.gauss</td>
      <td>Gaussian distribution.  mu is the mean, and si...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>random.lognormvariate</td>
      <td>Log normal distribution.  If you take the natu...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>random.normalvariate</td>
      <td>Normal distribution.  mu is the mean, and sigm...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>random.vonmisesvariate</td>
      <td>mu is the mean angle, expressed in radians bet...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>random.paretovariate</td>
      <td>Pareto distribution.  alpha is the shape param...</td>
    </tr>
    <tr>
      <th>22</th>
      <td>random.weibullvariate</td>
      <td>Weibull distribution.  alpha is the scale para...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>random.Random</td>
      <td>Class that implements the default pseudo-rando...</td>
=======
 t pseudo-rando...</td>
>>>>>>> First commit
    </tr>
    <tr>
      <th>24</th>
      <td>random.SystemRandom</td>
      <td>Class that uses the os.urandom() function for ...</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Let make a CSV file from the dataframe

data.to_csv('random_function.csv')
```

**BONUS: if you want to target a specific attributes, for example `id="bookeeping-functions"` you can use the following code:**


```python
# Target specific attributes

#example = soup.body.findAll ('div', attrs = {'id' : 'bookeeping-functions'})
#print(example)    # you can get very specific result with BeautifulSoup
```

## II. Web Scraping Using Pandas 

Pandas is very useful! We can easily scrape data using the pandas `read_html()` function for your data science project. 

We will be web scraping NBA player stats data and perform a quick data exploration from the website [basketball-reference.com](https://www.basketball-reference.com).

### Get The URL

First, we want to check out the specific [URL](https://www.basketball-reference.com/leagues/NBA_2020_per_game.html) that we are going to scrape the data - the NBA Player Stats of season 2019-2020.




```python
# Method 1: only 1 year

# URL of the player stats in 2020

url = 'https://www.basketball-reference.com/leagues/NBA_2020_per_game.html'
url
```




    'https://www.basketball-reference.com/leagues/NBA_2020_per_game.html'




```python
# Method 2: multiple years

years = ['2016', '2017', '2018', '2019', '2020']
str = 'https://www.basketball-reference.com/leagues/NBA_{}_per_game.html'

for year in years:
    url = str.format(year)
    print(url)
```

    https://www.basketball-reference.com/leagues/NBA_2016_per_game.html
    https://www.basketball-reference.com/leagues/NBA_2017_per_game.html
    https://www.basketball-reference.com/leagues/NBA_2018_per_game.html
    https://www.basketball-reference.com/leagues/NBA_2019_per_game.html
    https://www.basketball-reference.com/leagues/NBA_2020_per_game.html


### Read The HTML Webpage Into Pandas


```python
# Let check URL of the player stats in 2020

url = 'https://www.basketball-reference.com/leagues/NBA_2020_per_game.html'

# Using pd.read_html()

df = pd.read_html(url, header = 0)

print(df)
```

    [      Rk                    Player Pos Age   Tm   G  GS    MP   FG   FGA  ...  \
    0      1              Steven Adams   C  26  OKC  63  63  26.7  4.5   7.6  ...   
    1      2               Bam Adebayo  PF  22  MIA  72  72  33.6  6.1  11.0  ...   
    2      3         LaMarcus Aldridge   C  34  SAS  53  53  33.1  7.4  15.0  ...   
    3      4            Kyle Alexander   C  23  MIA   2   0   6.5  0.5   1.0  ...   
    4      5  Nickeil Alexander-Walker  SG  21  NOP  47   1  12.6  2.1   5.7  ...   
    ..   ...                       ...  ..  ..  ...  ..  ..   ...  ...   ...  ...   
    672  525                Trae Young  PG  21  ATL  60  60  35.3  9.1  20.8  ...   
    673  526               Cody Zeller   C  27  CHO  58  39  23.1  4.3   8.3  ...   
    674  527              Tyler Zeller   C  30  SAS   2   0   2.0  0.5   2.0  ...   
    675  528                Ante Žižić   C  23  CLE  22   0  10.0  1.9   3.3  ...   
    676  529               Ivica Zubac   C  22  LAC  72  70  18.4  3.3   5.3  ...   
    
          FT%  ORB  DRB   TRB  AST  STL  BLK  TOV   PF   PTS  
    0    .582  3.3  6.0   9.3  2.3  0.8  1.1  1.5  1.9  10.9  
    1    .691  2.4  7.8  10.2  5.1  1.1  1.3  2.8  2.5  15.9  
    2    .827  1.9  5.5   7.4  2.4  0.7  1.6  1.4  2.4  18.9  
    3     NaN  1.0  0.5   1.5  0.0  0.0  0.0  0.5  0.5   1.0  
    4    .676  0.2  1.6   1.8  1.9  0.4  0.2  1.1  1.2   5.7  
    ..    ...  ...  ...   ...  ...  ...  ...  ...  ...   ...  
    672  .860  0.5  3.7   4.3  9.3  1.1  0.1  4.8  1.7  29.6  
    673  .682  2.8  4.3   7.1  1.5  0.7  0.4  1.3  2.4  11.1  
    674   NaN  1.5  0.5   2.0  0.0  0.0  0.0  0.0  0.0   1.0  
    675  .737  0.8  2.2   3.0  0.3  0.3  0.2  0.5  1.2   4.4  
    676  .747  2.7  4.8   7.5  1.1  0.2  0.9  0.8  2.3   8.3  
    
    [677 rows x 30 columns]]


**It looks a little bit messy. What we actually have here is a list of DataFrames. We can beautify this object using Pandas (without any additional libraries!)**


```python
# Check number of DataFrames in this list

print(f'number of tables in df: {len(df)}') 

print('================')

# Since there is only 1, pull out the 0th element:
df[0].head(20)
```

    number of tables in df: 1
    ================





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Rk</th>
      <th>Player</th>
      <th>Pos</th>
      <th>Age</th>
      <th>Tm</th>
      <th>G</th>
      <th>GS</th>
      <th>MP</th>
      <th>FG</th>
      <th>FGA</th>
      <th>...</th>
      <th>FT%</th>
      <th>ORB</th>
      <th>DRB</th>
      <th>TRB</th>
      <th>AST</th>
      <th>STL</th>
      <th>BLK</th>
      <th>TOV</th>
      <th>PF</th>
      <th>PTS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Steven Adams</td>
      <td>C</td>
      <td>26</td>
      <td>OKC</td>
      <td>63</td>
      <td>63</td>
      <td>26.7</td>
      <td>4.5</td>
      <td>7.6</td>
      <td>...</td>
      <td>.582</td>
      <td>3.3</td>
      <td>6.0</td>
      <td>9.3</td>
      <td>2.3</td>
      <td>0.8</td>
      <td>1.1</td>
      <td>1.5</td>
      <td>1.9</td>
      <td>10.9</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Bam Adebayo</td>
      <td>PF</td>
      <td>22</td>
      <td>MIA</td>
      <td>72</td>
      <td>72</td>
      <td>33.6</td>
      <td>6.1</td>
      <td>11.0</td>
      <td>...</td>
      <td>.691</td>
      <td>2.4</td>
      <td>7.8</td>
      <td>10.2</td>
      <td>5.1</td>
      <td>1.1</td>
      <td>1.3</td>
      <td>2.8</td>
      <td>2.5</td>
      <td>15.9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>LaMarcus Aldridge</td>
      <td>C</td>
      <td>34</td>
      <td>SAS</td>
      <td>53</td>
      <td>53</td>
      <td>33.1</td>
      <td>7.4</td>
      <td>15.0</td>
      <td>...</td>
      <td>.827</td>
      <td>1.9</td>
      <td>5.5</td>
      <td>7.4</td>
      <td>2.4</td>
      <td>0.7</td>
      <td>1.6</td>
      <td>1.4</td>
      <td>2.4</td>
      <td>18.9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Kyle Alexander</td>
      <td>C</td>
      <td>23</td>
      <td>MIA</td>
      <td>2</td>
      <td>0</td>
      <td>6.5</td>
      <td>0.5</td>
      <td>1.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.5</td>
      <td>1.5</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Nickeil Alexander-Walker</td>
      <td>SG</td>
      <td>21</td>
      <td>NOP</td>
      <td>47</td>
      <td>1</td>
      <td>12.6</td>
      <td>2.1</td>
      <td>5.7</td>
      <td>...</td>
      <td>.676</td>
      <td>0.2</td>
      <td>1.6</td>
      <td>1.8</td>
      <td>1.9</td>
      <td>0.4</td>
      <td>0.2</td>
      <td>1.1</td>
      <td>1.2</td>
      <td>5.7</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Grayson Allen</td>
      <td>SG</td>
      <td>24</td>
      <td>MEM</td>
      <td>38</td>
      <td>0</td>
      <td>18.9</td>
      <td>3.1</td>
      <td>6.6</td>
      <td>...</td>
      <td>.867</td>
      <td>0.2</td>
      <td>2.0</td>
      <td>2.2</td>
      <td>1.4</td>
      <td>0.3</td>
      <td>0.1</td>
      <td>0.9</td>
      <td>1.4</td>
      <td>8.7</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Jarrett Allen</td>
      <td>C</td>
      <td>21</td>
      <td>BRK</td>
      <td>70</td>
      <td>64</td>
      <td>26.5</td>
      <td>4.3</td>
      <td>6.6</td>
      <td>...</td>
      <td>.633</td>
      <td>3.1</td>
      <td>6.5</td>
      <td>9.6</td>
      <td>1.6</td>
      <td>0.6</td>
      <td>1.3</td>
      <td>1.1</td>
      <td>2.3</td>
      <td>11.1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Kadeem Allen</td>
      <td>PG</td>
      <td>27</td>
      <td>NYK</td>
      <td>10</td>
      <td>0</td>
      <td>11.7</td>
      <td>1.9</td>
      <td>4.4</td>
      <td>...</td>
      <td>.636</td>
      <td>0.2</td>
      <td>0.7</td>
      <td>0.9</td>
      <td>2.1</td>
      <td>0.5</td>
      <td>0.2</td>
      <td>0.8</td>
      <td>0.7</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>Al-Farouq Aminu</td>
      <td>PF</td>
      <td>29</td>
      <td>ORL</td>
      <td>18</td>
      <td>2</td>
      <td>21.1</td>
      <td>1.4</td>
      <td>4.8</td>
      <td>...</td>
      <td>.655</td>
      <td>1.3</td>
      <td>3.5</td>
      <td>4.8</td>
      <td>1.2</td>
      <td>1.0</td>
      <td>0.4</td>
      <td>0.9</td>
      <td>1.5</td>
      <td>4.3</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>Justin Anderson</td>
      <td>SG</td>
      <td>26</td>
      <td>BRK</td>
      <td>10</td>
      <td>1</td>
      <td>10.7</td>
      <td>1.0</td>
      <td>3.8</td>
      <td>...</td>
      <td>.500</td>
      <td>0.1</td>
      <td>2.0</td>
      <td>2.1</td>
      <td>0.8</td>
      <td>0.0</td>
      <td>0.6</td>
      <td>0.4</td>
      <td>1.3</td>
      <td>2.8</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>Kyle Anderson</td>
      <td>SF</td>
      <td>26</td>
      <td>MEM</td>
      <td>67</td>
      <td>28</td>
      <td>19.9</td>
      <td>2.3</td>
      <td>4.9</td>
      <td>...</td>
      <td>.667</td>
      <td>0.9</td>
      <td>3.4</td>
      <td>4.3</td>
      <td>2.4</td>
      <td>0.8</td>
      <td>0.6</td>
      <td>1.0</td>
      <td>1.7</td>
      <td>5.8</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>Ryan Anderson</td>
      <td>C</td>
      <td>31</td>
      <td>HOU</td>
      <td>2</td>
      <td>0</td>
      <td>7.0</td>
      <td>1.0</td>
      <td>3.5</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>3.5</td>
      <td>3.5</td>
      <td>1.0</td>
      <td>0.5</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>Giannis Antetokounmpo</td>
      <td>PF</td>
      <td>25</td>
      <td>MIL</td>
      <td>63</td>
      <td>63</td>
      <td>30.4</td>
      <td>10.9</td>
      <td>19.7</td>
      <td>...</td>
      <td>.633</td>
      <td>2.2</td>
      <td>11.4</td>
      <td>13.6</td>
      <td>5.6</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.7</td>
      <td>3.1</td>
      <td>29.5</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>Kostas Antetokounmpo</td>
      <td>PF</td>
      <td>22</td>
      <td>LAL</td>
      <td>5</td>
      <td>0</td>
      <td>4.0</td>
      <td>0.6</td>
      <td>0.6</td>
      <td>...</td>
      <td>.500</td>
      <td>0.4</td>
      <td>0.2</td>
      <td>0.6</td>
      <td>0.4</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.2</td>
      <td>0.4</td>
      <td>1.4</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>Thanasis Antetokounmpo</td>
      <td>SF</td>
      <td>27</td>
      <td>MIL</td>
      <td>20</td>
      <td>2</td>
      <td>6.5</td>
      <td>1.2</td>
      <td>2.4</td>
      <td>...</td>
      <td>.412</td>
      <td>0.6</td>
      <td>0.6</td>
      <td>1.2</td>
      <td>0.8</td>
      <td>0.4</td>
      <td>0.1</td>
      <td>0.6</td>
      <td>0.9</td>
      <td>2.8</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>Carmelo Anthony</td>
      <td>PF</td>
      <td>35</td>
      <td>POR</td>
      <td>58</td>
      <td>58</td>
      <td>32.8</td>
      <td>5.8</td>
      <td>13.5</td>
      <td>...</td>
      <td>.845</td>
      <td>1.2</td>
      <td>5.1</td>
      <td>6.3</td>
      <td>1.5</td>
      <td>0.8</td>
      <td>0.5</td>
      <td>1.7</td>
      <td>2.9</td>
      <td>15.4</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>OG Anunoby</td>
      <td>SF</td>
      <td>22</td>
      <td>TOR</td>
      <td>69</td>
      <td>68</td>
      <td>29.9</td>
      <td>4.1</td>
      <td>8.2</td>
      <td>...</td>
      <td>.706</td>
      <td>1.2</td>
      <td>4.1</td>
      <td>5.3</td>
      <td>1.6</td>
      <td>1.4</td>
      <td>0.7</td>
      <td>1.1</td>
      <td>2.4</td>
      <td>10.6</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>Ryan Arcidiacono</td>
      <td>PG</td>
      <td>25</td>
      <td>CHI</td>
      <td>58</td>
      <td>4</td>
      <td>16.0</td>
      <td>1.6</td>
      <td>3.8</td>
      <td>...</td>
      <td>.711</td>
      <td>0.3</td>
      <td>1.6</td>
      <td>1.9</td>
      <td>1.7</td>
      <td>0.5</td>
      <td>0.1</td>
      <td>0.6</td>
      <td>1.7</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>Trevor Ariza</td>
      <td>SF</td>
      <td>34</td>
      <td>TOT</td>
      <td>53</td>
      <td>21</td>
      <td>28.2</td>
      <td>2.7</td>
      <td>6.1</td>
      <td>...</td>
      <td>.838</td>
      <td>0.6</td>
      <td>4.0</td>
      <td>4.6</td>
      <td>1.7</td>
      <td>1.3</td>
      <td>0.3</td>
      <td>1.1</td>
      <td>2.1</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>Trevor Ariza</td>
      <td>SF</td>
      <td>34</td>
      <td>SAC</td>
      <td>32</td>
      <td>0</td>
      <td>24.7</td>
      <td>2.0</td>
      <td>5.2</td>
      <td>...</td>
      <td>.778</td>
      <td>0.7</td>
      <td>3.9</td>
      <td>4.6</td>
      <td>1.6</td>
      <td>1.1</td>
      <td>0.2</td>
      <td>0.9</td>
      <td>2.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>19</td>
      <td>Trevor Ariza</td>
      <td>SF</td>
      <td>34</td>
      <td>POR</td>
      <td>21</td>
      <td>21</td>
      <td>33.4</td>
      <td>3.7</td>
      <td>7.6</td>
      <td>...</td>
      <td>.872</td>
      <td>0.6</td>
      <td>4.1</td>
      <td>4.8</td>
      <td>2.0</td>
      <td>1.6</td>
      <td>0.4</td>
      <td>1.3</td>
      <td>2.3</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>20</td>
      <td>D.J. Augustin</td>
      <td>PG</td>
      <td>32</td>
      <td>ORL</td>
      <td>57</td>
      <td>13</td>
      <td>24.9</td>
      <td>3.2</td>
      <td>8.1</td>
      <td>...</td>
      <td>.890</td>
      <td>0.4</td>
      <td>1.8</td>
      <td>2.1</td>
      <td>4.6</td>
      <td>0.6</td>
      <td>0.0</td>
      <td>1.5</td>
      <td>1.3</td>
      <td>10.5</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Rk</td>
      <td>Player</td>
      <td>Pos</td>
      <td>Age</td>
      <td>Tm</td>
      <td>G</td>
      <td>GS</td>
      <td>MP</td>
      <td>FG</td>
      <td>FGA</td>
      <td>...</td>
      <td>FT%</td>
      <td>ORB</td>
      <td>DRB</td>
      <td>TRB</td>
      <td>AST</td>
      <td>STL</td>
      <td>BLK</td>
      <td>TOV</td>
      <td>PF</td>
      <td>PTS</td>
    </tr>
    <tr>
      <th>23</th>
      <td>21</td>
      <td>Deandre Ayton</td>
      <td>C</td>
      <td>21</td>
      <td>PHO</td>
      <td>38</td>
      <td>32</td>
      <td>32.5</td>
      <td>8.2</td>
      <td>14.9</td>
      <td>...</td>
      <td>.753</td>
      <td>3.9</td>
      <td>7.6</td>
      <td>11.5</td>
      <td>1.9</td>
      <td>0.7</td>
      <td>1.5</td>
      <td>2.1</td>
      <td>3.1</td>
      <td>18.2</td>
    </tr>
    <tr>
      <th>24</th>
      <td>22</td>
      <td>Dwayne Bacon</td>
      <td>SG</td>
      <td>24</td>
      <td>CHO</td>
      <td>39</td>
      <td>11</td>
      <td>17.6</td>
      <td>2.2</td>
      <td>6.3</td>
      <td>...</td>
      <td>.660</td>
      <td>0.4</td>
      <td>2.2</td>
      <td>2.6</td>
      <td>1.3</td>
      <td>0.6</td>
      <td>0.1</td>
      <td>0.9</td>
      <td>1.3</td>
      <td>5.7</td>
    </tr>
  </tbody>
</table>
<p>25 rows × 30 columns</p>
</div>



Wow! You'll notice that there are some missing values (NaN) and multiple occurences of some player names because they have been a part of different teams in the same year.

### Data Cleaning

**We can see on the website that the header repeats itself in every 20 players. We'll have to remove the subsequent headers and keep only the first header:**

<br>
<br>
<img src = "https://docs.google.com/uc?export=download&id=1CEQs7TNFr4Nak0sQK10QYXl06uXcvrLN" />

<br>
<br>


```python
# Assigns the table in a variable df_2020

df_2020 = df[0]

# Let check the table header which is presented multiple times in several rows

df_2020[df_2020.Age == 'Age'].head() #  All the subsequent table header selected for this entire dataframe!

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Rk</th>
      <th>Player</th>
      <th>Pos</th>
      <th>Age</th>
      <th>Tm</th>
      <th>G</th>
      <th>GS</th>
      <th>MP</th>
      <th>FG</th>
      <th>FGA</th>
      <th>...</th>
      <th>FT%</th>
      <th>ORB</th>
      <th>DRB</th>
      <th>TRB</th>
      <th>AST</th>
      <th>STL</th>
      <th>BLK</th>
      <th>TOV</th>
      <th>PF</th>
      <th>PTS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>22</th>
      <td>Rk</td>
      <td>Player</td>
      <td>Pos</td>
      <td>Age</td>
      <td>Tm</td>
      <td>G</td>
      <td>GS</td>
      <td>MP</td>
      <td>FG</td>
      <td>FGA</td>
      <td>...</td>
      <td>FT%</td>
      <td>ORB</td>
      <td>DRB</td>
      <td>TRB</td>
      <td>AST</td>
      <td>STL</td>
      <td>BLK</td>
      <td>TOV</td>
      <td>PF</td>
      <td>PTS</td>
    </tr>
    <tr>
      <th>53</th>
      <td>Rk</td>
      <td>Player</td>
      <td>Pos</td>
      <td>Age</td>
      <td>Tm</td>
      <td>G</td>
      <td>GS</td>
      <td>MP</td>
      <td>FG</td>
      <td>FGA</td>
      <td>...</td>
      <td>FT%</td>
      <td>ORB</td>
      <td>DRB</td>
      <td>TRB</td>
      <td>AST</td>
      <td>STL</td>
      <td>BLK</td>
      <td>TOV</td>
      <td>PF</td>
      <td>PTS</td>
    </tr>
    <tr>
      <th>76</th>
      <td>Rk</td>
      <td>Player</td>
      <td>Pos</td>
      <td>Age</td>
      <td>Tm</td>
      <td>G</td>
      <td>GS</td>
      <td>MP</td>
      <td>FG</td>
      <td>FGA</td>
      <td>...</td>
      <td>FT%</td>
      <td>ORB</td>
      <td>DRB</td>
      <td>TRB</td>
      <td>AST</td>
      <td>STL</td>
      <td>BLK</td>
      <td>TOV</td>
      <td>PF</td>
      <td>PTS</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Rk</td>
      <td>Player</td>
      <td>Pos</td>
      <td>Age</td>
      <td>Tm</td>
      <td>G</td>
      <td>GS</td>
      <td>MP</td>
      <td>FG</td>
      <td>FGA</td>
      <td>...</td>
      <td>FT%</td>
      <td>ORB</td>
      <td>DRB</td>
      <td>TRB</td>
      <td>AST</td>
      <td>STL</td>
      <td>BLK</td>
      <td>TOV</td>
      <td>PF</td>
      <td>PTS</td>
    </tr>
    <tr>
      <th>130</th>
      <td>Rk</td>
      <td>Player</td>
      <td>Pos</td>
      <td>Age</td>
      <td>Tm</td>
      <td>G</td>
      <td>GS</td>
      <td>MP</td>
      <td>FG</td>
      <td>FGA</td>
      <td>...</td>
      <td>FT%</td>
      <td>ORB</td>
      <td>DRB</td>
      <td>TRB</td>
      <td>AST</td>
      <td>STL</td>
      <td>BLK</td>
      <td>TOV</td>
      <td>PF</td>
      <td>PTS</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 30 columns</p>
</div>




```python
# Checking the length for how many header we have:

print(f' total numbers of redundant headers: {len(df_2020[df_2020.Age == "Age"])} ')

# Drop the redundant headers in the dataframe:
df_2020_new = df_2020.drop(df_2020[df_2020.Age == 'Age'].index)

# Compare before and after dropping redundant headers with numbers of rows:

print(f' total rows of df_2020:     {df_2020.shape[0]} ')
print(f' total rows of df_2020_new: {df_2020_new.shape[0]} ')
print('===========================================')

df_2020_new.head(20)
```

     total numbers of redundant headers: 26 
     total rows of df_2020:     677 
     total rows of df_2020_new: 651 
    ===========================================





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Rk</th>
      <th>Player</th>
      <th>Pos</th>
      <th>Age</th>
      <th>Tm</th>
      <th>G</th>
      <th>GS</th>
      <th>MP</th>
      <th>FG</th>
      <th>FGA</th>
      <th>...</th>
      <th>FT%</th>
      <th>ORB</th>
      <th>DRB</th>
      <th>TRB</th>
      <th>AST</th>
      <th>STL</th>
      <th>BLK</th>
      <th>TOV</th>
      <th>PF</th>
      <th>PTS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Steven Adams</td>
      <td>C</td>
      <td>26</td>
      <td>OKC</td>
      <td>63</td>
      <td>63</td>
      <td>26.7</td>
      <td>4.5</td>
      <td>7.6</td>
      <td>...</td>
      <td>.582</td>
      <td>3.3</td>
      <td>6.0</td>
      <td>9.3</td>
      <td>2.3</td>
      <td>0.8</td>
      <td>1.1</td>
      <td>1.5</td>
      <td>1.9</td>
      <td>10.9</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Bam Adebayo</td>
      <td>PF</td>
      <td>22</td>
      <td>MIA</td>
      <td>72</td>
      <td>72</td>
      <td>33.6</td>
      <td>6.1</td>
      <td>11.0</td>
      <td>...</td>
      <td>.691</td>
      <td>2.4</td>
      <td>7.8</td>
      <td>10.2</td>
      <td>5.1</td>
      <td>1.1</td>
      <td>1.3</td>
      <td>2.8</td>
      <td>2.5</td>
      <td>15.9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>LaMarcus Aldridge</td>
      <td>C</td>
      <td>34</td>
      <td>SAS</td>
      <td>53</td>
      <td>53</td>
      <td>33.1</td>
      <td>7.4</td>
      <td>15.0</td>
      <td>...</td>
      <td>.827</td>
      <td>1.9</td>
      <td>5.5</td>
      <td>7.4</td>
      <td>2.4</td>
      <td>0.7</td>
      <td>1.6</td>
      <td>1.4</td>
      <td>2.4</td>
      <td>18.9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Kyle Alexander</td>
      <td>C</td>
      <td>23</td>
      <td>MIA</td>
      <td>2</td>
      <td>0</td>
      <td>6.5</td>
      <td>0.5</td>
      <td>1.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.5</td>
      <td>1.5</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Nickeil Alexander-Walker</td>
      <td>SG</td>
      <td>21</td>
      <td>NOP</td>
      <td>47</td>
      <td>1</td>
      <td>12.6</td>
      <td>2.1</td>
      <td>5.7</td>
      <td>...</td>
      <td>.676</td>
      <td>0.2</td>
      <td>1.6</td>
      <td>1.8</td>
      <td>1.9</td>
      <td>0.4</td>
      <td>0.2</td>
      <td>1.1</td>
      <td>1.2</td>
      <td>5.7</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Grayson Allen</td>
      <td>SG</td>
      <td>24</td>
      <td>MEM</td>
      <td>38</td>
      <td>0</td>
      <td>18.9</td>
      <td>3.1</td>
      <td>6.6</td>
      <td>...</td>
      <td>.867</td>
      <td>0.2</td>
      <td>2.0</td>
      <td>2.2</td>
      <td>1.4</td>
      <td>0.3</td>
      <td>0.1</td>
      <td>0.9</td>
      <td>1.4</td>
      <td>8.7</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Jarrett Allen</td>
      <td>C</td>
      <td>21</td>
      <td>BRK</td>
      <td>70</td>
      <td>64</td>
      <td>26.5</td>
      <td>4.3</td>
      <td>6.6</td>
      <td>...</td>
      <td>.633</td>
      <td>3.1</td>
      <td>6.5</td>
      <td>9.6</td>
      <td>1.6</td>
      <td>0.6</td>
      <td>1.3</td>
      <td>1.1</td>
      <td>2.3</td>
      <td>11.1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Kadeem Allen</td>
      <td>PG</td>
      <td>27</td>
      <td>NYK</td>
      <td>10</td>
      <td>0</td>
      <td>11.7</td>
      <td>1.9</td>
      <td>4.4</td>
      <td>...</td>
      <td>.636</td>
      <td>0.2</td>
      <td>0.7</td>
      <td>0.9</td>
      <td>2.1</td>
      <td>0.5</td>
      <td>0.2</td>
      <td>0.8</td>
      <td>0.7</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>Al-Farouq Aminu</td>
      <td>PF</td>
      <td>29</td>
      <td>ORL</td>
      <td>18</td>
      <td>2</td>
      <td>21.1</td>
      <td>1.4</td>
      <td>4.8</td>
      <td>...</td>
      <td>.655</td>
      <td>1.3</td>
      <td>3.5</td>
      <td>4.8</td>
      <td>1.2</td>
      <td>1.0</td>
      <td>0.4</td>
      <td>0.9</td>
      <td>1.5</td>
      <td>4.3</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>Justin Anderson</td>
      <td>SG</td>
      <td>26</td>
      <td>BRK</td>
      <td>10</td>
      <td>1</td>
      <td>10.7</td>
      <td>1.0</td>
      <td>3.8</td>
      <td>...</td>
      <td>.500</td>
      <td>0.1</td>
      <td>2.0</td>
      <td>2.1</td>
      <td>0.8</td>
      <td>0.0</td>
      <td>0.6</td>
      <td>0.4</td>
      <td>1.3</td>
      <td>2.8</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>Kyle Anderson</td>
      <td>SF</td>
      <td>26</td>
      <td>MEM</td>
      <td>67</td>
      <td>28</td>
      <td>19.9</td>
      <td>2.3</td>
      <td>4.9</td>
      <td>...</td>
      <td>.667</td>
      <td>0.9</td>
      <td>3.4</td>
      <td>4.3</td>
      <td>2.4</td>
      <td>0.8</td>
      <td>0.6</td>
      <td>1.0</td>
      <td>1.7</td>
      <td>5.8</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>Ryan Anderson</td>
      <td>C</td>
      <td>31</td>
      <td>HOU</td>
      <td>2</td>
      <td>0</td>
      <td>7.0</td>
      <td>1.0</td>
      <td>3.5</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>3.5</td>
      <td>3.5</td>
      <td>1.0</td>
      <td>0.5</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>Giannis Antetokounmpo</td>
      <td>PF</td>
      <td>25</td>
      <td>MIL</td>
      <td>63</td>
      <td>63</td>
      <td>30.4</td>
      <td>10.9</td>
      <td>19.7</td>
      <td>...</td>
      <td>.633</td>
      <td>2.2</td>
      <td>11.4</td>
      <td>13.6</td>
      <td>5.6</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.7</td>
      <td>3.1</td>
      <td>29.5</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>Kostas Antetokounmpo</td>
      <td>PF</td>
      <td>22</td>
      <td>LAL</td>
      <td>5</td>
      <td>0</td>
      <td>4.0</td>
      <td>0.6</td>
      <td>0.6</td>
      <td>...</td>
      <td>.500</td>
      <td>0.4</td>
      <td>0.2</td>
      <td>0.6</td>
      <td>0.4</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.2</td>
      <td>0.4</td>
      <td>1.4</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>Thanasis Antetokounmpo</td>
      <td>SF</td>
      <td>27</td>
      <td>MIL</td>
      <td>20</td>
      <td>2</td>
      <td>6.5</td>
      <td>1.2</td>
      <td>2.4</td>
      <td>...</td>
      <td>.412</td>
      <td>0.6</td>
      <td>0.6</td>
      <td>1.2</td>
      <td>0.8</td>
      <td>0.4</td>
      <td>0.1</td>
      <td>0.6</td>
      <td>0.9</td>
      <td>2.8</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>Carmelo Anthony</td>
      <td>PF</td>
      <td>35</td>
      <td>POR</td>
      <td>58</td>
      <td>58</td>
      <td>32.8</td>
      <td>5.8</td>
      <td>13.5</td>
      <td>...</td>
      <td>.845</td>
      <td>1.2</td>
      <td>5.1</td>
      <td>6.3</td>
      <td>1.5</td>
      <td>0.8</td>
      <td>0.5</td>
      <td>1.7</td>
      <td>2.9</td>
      <td>15.4</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>OG Anunoby</td>
      <td>SF</td>
      <td>22</td>
      <td>TOR</td>
      <td>69</td>
      <td>68</td>
      <td>29.9</td>
      <td>4.1</td>
      <td>8.2</td>
      <td>...</td>
      <td>.706</td>
      <td>1.2</td>
      <td>4.1</td>
      <td>5.3</td>
      <td>1.6</td>
      <td>1.4</td>
      <td>0.7</td>
      <td>1.1</td>
      <td>2.4</td>
      <td>10.6</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>Ryan Arcidiacono</td>
      <td>PG</td>
      <td>25</td>
      <td>CHI</td>
      <td>58</td>
      <td>4</td>
      <td>16.0</td>
      <td>1.6</td>
      <td>3.8</td>
      <td>...</td>
      <td>.711</td>
      <td>0.3</td>
      <td>1.6</td>
      <td>1.9</td>
      <td>1.7</td>
      <td>0.5</td>
      <td>0.1</td>
      <td>0.6</td>
      <td>1.7</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>Trevor Ariza</td>
      <td>SF</td>
      <td>34</td>
      <td>TOT</td>
      <td>53</td>
      <td>21</td>
      <td>28.2</td>
      <td>2.7</td>
      <td>6.1</td>
      <td>...</td>
      <td>.838</td>
      <td>0.6</td>
      <td>4.0</td>
      <td>4.6</td>
      <td>1.7</td>
      <td>1.3</td>
      <td>0.3</td>
      <td>1.1</td>
      <td>2.1</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>Trevor Ariza</td>
      <td>SF</td>
      <td>34</td>
      <td>SAC</td>
      <td>32</td>
      <td>0</td>
      <td>24.7</td>
      <td>2.0</td>
      <td>5.2</td>
      <td>...</td>
      <td>.778</td>
      <td>0.7</td>
      <td>3.9</td>
      <td>4.6</td>
      <td>1.6</td>
      <td>1.1</td>
      <td>0.2</td>
      <td>0.9</td>
      <td>2.0</td>
      <td>6.0</td>
    </tr>
  </tbody>
</table>
<p>20 rows × 30 columns</p>
</div>



### Quick Exploratory Data Analysis


```python
# Making a simple histogram

plt.figure(figsize=(10,8))

sns.distplot(df_2020_new.PTS,    # Checking frequency of the player points
            kde= False,          # Should be False because we want to retain the original frequency ( "kde=True" => it will be the probability)
            hist_kws = dict( edgecolor = 'black', linewidth=2))  

plt.title('HISTOGRAM OF PLAYER POINTS PER GAME IN THE 2020 NBA SEASON')
plt.ylabel('NUMBERS OF PLAYERS')
plt.xlabel('POINTS PER GAME')
plt.show()
```


    
![png](output_54_0.png)
    


From the histogram, we can see: 
- There are about 57 players having between 0 and 1 point.
- There are less than 10 players who had 30 points.
<<<<<<< HEAD


```python
# Retrieve the first song's URL
r.json()["response"]["songs"][0]["url"]
```




    'https://genius.com/Christmas-songs-adeste-fideles-lyrics'




```python
# Retrieve each song's URL
urls = [song['url'] for song in r.json()['response']['songs']]
urls
```




    ['https://genius.com/Christmas-songs-adeste-fideles-lyrics',
     'https://genius.com/Christmas-songs-all-i-want-for-christmas-is-you-lyrics',
     'https://genius.com/Christmas-songs-amazing-grace-lyrics',
     'https://genius.com/Christmas-songs-angels-we-have-heard-on-high-lyrics',
     'https://genius.com/Christmas-songs-as-lately-we-watched-lyrics',
     'https://genius.com/Christmas-songs-auld-lang-syne-lyrics',
     'https://genius.com/Christmas-songs-ave-maria-lyrics',
     'https://genius.com/Christmas-songs-away-in-a-manger-lyrics',
     'https://genius.com/Christmas-songs-baby-its-cold-outside-lyrics',
     'https://genius.com/Christmas-songs-bells-of-christmas-lyrics',
     'https://genius.com/Christmas-songs-blue-christmas-lyrics',
     'https://genius.com/Christmas-songs-brahms-lullaby-lyrics',
     'https://genius.com/Christmas-songs-buon-natale-merry-christmas-to-you-lyrics',
     'https://genius.com/Christmas-songs-carol-of-the-bells-lyrics',
     'https://genius.com/Christmas-songs-celebration-lyrics',
     'https://genius.com/Christmas-songs-christmas-all-over-again-lyrics',
     'https://genius.com/Christmas-songs-christmas-and-you-lyrics',
     'https://genius.com/Christmas-songs-christmas-at-our-house-lyrics',
     'https://genius.com/Christmas-songs-christmas-auld-lang-syne-lyrics',
     'https://genius.com/Christmas-songs-christmas-bells-lyrics',
     'https://genius.com/Christmas-songs-christmas-bride-lyrics',
     'https://genius.com/Christmas-songs-christmas-canon-lyrics',
     'https://genius.com/Christmas-songs-christmas-cards-lyrics',
     'https://genius.com/Christmas-songs-christmas-concerto-lyrics',
     'https://genius.com/Christmas-songs-christmas-dinner-lyrics',
     'https://genius.com/Christmas-songs-christmas-dreaming-a-little-early-this-year-lyrics',
     'https://genius.com/Christmas-songs-christmas-in-my-hometown-lyrics',
     'https://genius.com/Christmas-songs-christmas-is-a-feeling-in-your-heart-lyrics',
     'https://genius.com/Christmas-songs-christmas-is-coming-lyrics',
     'https://genius.com/Christmas-songs-christmas-island-lyrics',
     'https://genius.com/Christmas-songs-christmas-jazz-lyrics',
     'https://genius.com/Christmas-songs-christmas-lullaby-lyrics',
     'https://genius.com/Christmas-songs-christmas-memories-lyrics',
     'https://genius.com/Christmas-songs-christmas-present-lyrics',
     'https://genius.com/Christmas-songs-christmas-spirit-lyrics',
     'https://genius.com/Christmas-songs-christmas-time-lyrics',
     'https://genius.com/Christmas-songs-christmas-time-is-here-lyrics',
     'https://genius.com/Christmas-songs-deck-the-halls-lyrics',
     'https://genius.com/Christmas-songs-ding-dong-merrily-on-high-lyrics',
     'https://genius.com/Christmas-songs-dominick-the-donkey-lyrics',
     'https://genius.com/Christmas-songs-do-you-hear-what-i-hear-lyrics',
     'https://genius.com/Christmas-songs-driving-home-for-christmas-lyrics',
     'https://genius.com/Christmas-songs-feliz-navidad-lyrics',
     'https://genius.com/Christmas-songs-frosty-the-snowman-lyrics',
     'https://genius.com/Christmas-songs-fur-elise-lyrics']



This query limits its output to 20 results per page, but by looping through all these pages we could grab the URLs for all of Christmas Songs' songs, in a way that's much more streamlined than navigating to all of the album pages and scraping the URLs from there as we did above.


```python
def get_lyrics(urls):
    '''
    urls: list. Songs' urls
    ------------------------
    return: list. Songs' lyrics
    '''
    # define variable to hold the list of lyrics
    dedicated_lyrics = []
    
    # Loop through each URL in our list of URLs
    for url in urls:

        ### Because of peculiarities with how webpages on Genius are rendered, our get requests will not always produce the right output
        ### THe following while loop will download the page until the right results are produced

        # Initialize lyrics_block variable as None
        lyrics_block = None

        # Download webpage until lyrics are found
        while lyrics_block is None:

            # Make get request
            response = requests.get(url)

            # Soupify webpage
            soup = BeautifulSoup(response.content)

            # (Try to) find lyrics block on webpage; if successful, leave loop
            lyrics_block = soup.find('div', class_='lyrics')

            # Wait one second between each iteration so that we don't spam requests
            time.sleep(1)

        # Save lyrics
        lyrics = lyrics_block.text

        # Clean lyrics
        lyrics_cleaned = re.sub('\[.*\]', '', lyrics)

        # Append cleaned lyrics to master list
        dedicated_lyrics.append(lyrics_cleaned)

        # Print statement to check our progress
        print(f'Got the lyrics from {url}!')

        # Wait one second between each iteration so that we don't spam requests
        time.sleep(1)
        
    return dedicated_lyrics
```

And we've done it! Our data isn't yet in the most usable form, but we can now easily manipulate it with the Python functions we know.


```python
# number of songs collected
lyrics = get_lyrics(urls)

# Song 1
print(lyrics[0])
```

### A Final Note

When scraping, be considerate of your data source(s), and aware of any legal and technical obligations and limits! Websites often set limits on requests to discourage them, and scraping data does lie in a legally grey area which is expressly forbidden by some sites' Terms of Service.

If you're ever in doubt, you can add `robots.txt` at the end of a website's URL to check its permissions regarding scraping (*e.g.*, https://www.genius.com/robots.txt).
=======
>>>>>>> First commit
