---
title: "How to Scrape a Dashboard with Python"
layout: post
date: 2020-08-01
image: /assets/images/markdown.jpg
headerImage: false
tag:
- web scraping
- data science
- data analytics
star: true
category: blog
author: karlamejia
description: We’re going to learn how to scrape data from a dashboard using the Selenium and Beautiful Soup packages in Python.
---

Dashboard scraping is a useful skill to have when the only way to interact with the data you need is through a dashboard. We're going to learn how to scrape data from a dashboard using the [Selenium](https://selenium-python.readthedocs.io/) and [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) packages in Python. The Selenium package allows you to write Python code to automate web browser interaction, and the Beautiful Soup package allows you to easily pull data from the HTML code that produces the webpage you want to scrape.

Our goal is to scrape the [Fort Bend County Community Impact Dashboard](https://www.arcgis.com/apps/opsdashboard/index.html#/75133e049f584ae8b51dc6cba740009a) that visualizes the COVID-19 situation in Fort Bend County in Texas. We will extract the history of total tests performed and the daily case counts reported so that we can estimate the percent of positive cases in Fort Bend County.

Note that all of the code in this tutorial is written in Python version 3.6.2.

## Step 1: Import Python Packages, Modules and Methods
The first step is to import the Python packages, modules, and methods needed for dashboard scraping. The versions of the packages used in this tutorial are listed below.

{% gist karlamejia/1e4be87d46bb6eea116bd8aa66c61a2c %}


## Step 2: Scrape HTML Source Code



## Step 3: Parse Data from HTML



## Step 4: Calculate Positivity Rate




## Images

Markdown can also contain images. I'll need to add something here sometime.

{% highlight raw %}
![Markdowm Image][/image/url]
{% endhighlight %}

![Markdowm Image][5]

*Figure Caption*?

{% highlight raw %}
![Markdowm Image][/image/url]
<figcaption class="caption">Photo by John Doe</figcaption>
{% endhighlight %}

![Markdowm Image][5]
<figcaption class="caption">Photo by John Doe</figcaption>

*Bigger Images*?

{% highlight raw %}
![Markdowm Image][/image/url]{: class="bigger-image" }
{% endhighlight %}

![Markdowm Image][5]{: class="bigger-image" }

---

## Code

A HTML Example:

{% highlight html %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <h1>Just a test</h1>
</body>
</html>
{% endhighlight %}

A CSS Example:

{% highlight css %}
pre {
    padding: 10px;
    font-size: .8em;
    white-space: pre;
}

pre, table {
    width: 100%;
}

code, pre, tt {
    font-family: Monaco, Consolas, Inconsolata, monospace, sans-serif;
    background: rgba(0,0,0,.05);
}
{% endhighlight %}

A JS Example:

{% highlight js %}
// Sticky Header
$(window).scroll(function() {

    if ($(window).scrollTop() > 900 && !$("body").hasClass('show-menu')) {
        $('#hamburguer__open').fadeOut('fast');
    } else if (!$("body").hasClass('show-menu')) {
        $('#hamburguer__open').fadeIn('fast');
    }

});
{% endhighlight %}

[1]: https://daringfireball.net/projects/markdown/
[2]: https://www.fileformat.info/info/unicode/char/2163/index.htm
[3]: https://daringfireball.net/projects/markdown/basics
[4]: https://daringfireball.net/projects/markdown/syntax
[5]: https://kune.fr/wp-content/uploads/2013/10/ghost-blog.jpg
