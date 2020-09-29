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
externalLink: true
---

Dashboard scraping is a useful skill to have when the only way to interact with the data you need is through a dashboard. We're going to learn how to scrape data from a dashboard using the [Selenium](https://selenium-python.readthedocs.io/) and [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) packages in Python. The Selenium package allows you to write Python code to automate web browser interaction, and the Beautiful Soup package allows you to easily pull data from the HTML code that produces the webpage you want to scrape.

Our goal is to scrape the [Fort Bend County Community Impact Dashboard](https://www.arcgis.com/apps/opsdashboard/index.html#/75133e049f584ae8b51dc6cba740009a) that visualizes the COVID-19 situation in Fort Bend County in Texas. We will extract the history of total tests performed and the daily case counts reported so that we can estimate the percent of positive cases in Fort Bend County.

Note that all of the code in this tutorial is written in Python version 3.6.2.

## Step 1: Import Python Packages, Modules and Methods
The first step is to import the Python packages, modules, and methods needed for dashboard scraping. The versions of the packages used in this tutorial are listed below.

{% gist karlamejia/1e4be87d46bb6eea116bd8aa66c61a2c %}

{% gist karlamejia/8072efd27ed8528941c4c62fa39e6cf9 %}

## Step 2: Scrape HTML Source Code
The next step is to write Python code to automate our interaction with the dashboard. Before writing any code, we must look at the dashboard and inspect the source code to identify the HTML elements that contain the data we need. The dashboard source code refers to the HTML code that tells your browser how to render the dashboard web page. To view the dashboard source code, navigate to the dashboard and use the keyboard shortcut ``Ctrl+Shift+I``. An interactive panel containing the dashboard source code will appear.

Notice that the history of total tests performed and the daily case counts reported are only visible after clicking the "History" tab in the "Total Numbers of Tests Performed at County Sites" panel and the "Daily Case Count" tab in the "Confirmed Cases" panel, respectively. This means that we need to write Python code that automatically clicks on the "History" and "Daily Case Count" tabs so that the history of total tests performed and the daily case counts reported will be visible to Beautiful Soup.

![Fort Bend County Community Impact Dashboard on July 10th, 2020](/assets/images/dashboard-overview.png)

To find the HTML element that contains the "History" tab, use the shortcut ``Ctrl+Shift+C`` and then click on the "History" tab. You will see in the source code panel that the "History" tab is in a div element with ID "ember208".

![History Tab Source Code](/assets/images/history-html.png)

Following the same steps for the "Daily Case Count" tab, you will see that the "Daily Case Count" tab is in a div element with ID "ember238".

![Source Code of Daily Case Count Tab](/assets/images/daily-case-count-html.PNG)

Now that we have identified the elements we need, we can write code that:

Launches the dashboard in Chrome
1. Clicks on the "History" tab once the "History" tab finishes loading
2. Clicks on the "Daily Case Count" tab once the "Daily Case Count" tab finishes loading
3. Extracts the dashboard HTML source code
4. Exits Chrome

{% gist karlamejia/80d53775f7d8670f1c38bae3281195d7 %}

## Step 3: Parse Data from HTML
Now, we need to parse the HTML source code to extract the history of total tests performed and the daily case counts reported. We will begin by looking at the dashboard source code to identify the HTML elements that contain the data.

To find the div element that contains the history of total tests performed, use the ``Ctrl+Shift+C`` shortcut and then click in the general area of the "Testing Sites" plot. You will see in the source code that the entire plot is in the div element with ID "ember96".

![Source Code of Testing Sites Plot](/assets/images/history-plot.png)

If you hover over a specific data point, a label containing the date and number of tests performed will appear. Use the ``Ctrl+Shift+C`` shortcut and click on a specific data point. You will see that the label text is stored as the aria-label attribute of a g element.

![Source Code of Testing Sites Data Labels](/assets/images/history-label.png)

Following the same steps for the daily case counts reported, you will see that the plot of daily case counts is in the div element with ID "ember143".

![Source Code of Daily Cases Based on Report Date Plot](/assets/images/daily-case-count-plot.png)

If you hover over a specific data point, a label containing the date and the number of positive cases reported will appear. Using the ``Ctrl+Shift+C`` shortcut, you will notice that the data are also stored in the aria-label attribute of g elements.

![Source Code of Daily Cases based on Report Date Data Labels](/assets/images/daily-case-count-label.png)

Once we have the elements that contain the data, we can write code that:

1. Finds the div element that contains the plot of the total tests performed and pulls the total tests performed data
2. Finds the div element that contains the plot of the daily case counts and pulls the daily case count data
3. Combines the data in a pandas dataframe and exports it to a CSV

{% gist karlamejia/595af92b82578c659d9e9ce0b2757174 %}

## Step 4: Calculate Positivity Rate
Now, we can finally estimate the COVID-19 positivity rate in Fort Bend County. We will divide the cases reported by the tests performed and calculate the 7-day moving averages. It is unclear from the dashboard whether the reported positive cases include cases that were determined through tests not conducted by the county (e.g. tests conducted at a hospital or clinic). It is also unclear when the tests for the positive cases were conducted since the dashboard only displays the reported case date. That is why the positivity rates derived from these data are only considered a proxy for the true positivity rate.

{% gist karlamejia/1267eb47a172e32982c13a809890514a %}

![Plot of Total Cases, Total Tests, and Positivity Rate in Fort Bend County](/assets/images/final-plot.png)

## Sources
1. [https://www.fbchealth.org/ncov/](https://www.fbchealth.org/ncov/)
2. [https://www.fortbendcountytx.gov/your-county/fort-bend-county-expands-covid-19-testing-site-to-all-residents](https://www.fortbendcountytx.gov/your-county/fort-bend-county-expands-covid-19-testing-site-to-all-residents)
3. [https://gov.texas.gov/news/post/governor-abbott-announces-phase-one-to-open-texas-establishes-statewide-minimum-standard-health-protocols](https://gov.texas.gov/news/post/governor-abbott-announces-phase-one-to-open-texas-establishes-statewide-minimum-standard-health-protocols)
4. [https://gov.texas.gov/news/post/governor-abbott-announces-phase-two-to-open-texas](https://gov.texas.gov/news/post/governor-abbott-announces-phase-two-to-open-texas)
5. [https://gov.texas.gov/news/post/governor-abbott-announces-phase-iii-to-open-texas](https://gov.texas.gov/news/post/governor-abbott-announces-phase-iii-to-open-texas)
