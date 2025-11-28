+++
date = '2025-11-26T19:43:22+02:00'
title = '[Devlog 0.1] Investment Portfolio'
[params]
  math = true
+++

### Investing
For the past few years, I've been getting into investing. Modern banking apps make it reasonably easy to get started. In the Baltics, if you have an account with Revolut or Swedbank, you can already invest in publicly traded companies.
A good starting point is investing in companies who's news you already follow for one reason or another. This way, information wise, you're already ahead of some shmucs who just follows the big trend.

### Problem
In spite of this, I've allowed my own portfolio to grow so diverse and unfocused that I only can keep up to date with a couple of favourites. The other positions are just flashy numbers that the banking app throws at me and every other finance serf with a modern app.
Pretty, Pretty, Shiny, Shiny.
![Google stock go brrr](/posts/devlog01/shinyGoogle.png)


### Goal
I want to make my own shiny numbers. And so I had a need for something :  
A tool takes an array of Symbols I've invested in and plots relevant company data onto a excel sheet. Inside Excel, I can play around with any new function I come with - or read in some nerdy investment book - speaks to me. If it does, I can add it to my tool.

### Plan 0.1
So what's the stack? I don't know yet, and honestly It doesn't matter.  Golang has been giving me noughty winks for a while now, so I'll go with that one, and learn as I go (double pun not intended).
So let's break the tool down :  
1. I wish to get a list of stock symbols that I'm currently invested in  
2. Get some data about the stocks company : Stock price, Yearly Income etc.  
3. Plot this data into excel   

### Let's make something
Revolut has a well-documented API but sadly endpoints about investments are yet to be seen.  
Fine. For now Let's add symbols by hand via CLI arguments.

I can't take the same approach when it comes to company data, but luckuly there's a some services that - on a very tight leash - let play around for free. Just to get the ball rolling, I picked the first one on the search results : 
[Financial Modeling prep](https://site.financialmodelingprep.com/developer/docs)
  
Their docs are detailed and the endpoints are RESTful so they seem make sense - good enough to start with and replace with something more sustainable later.

Finnaly, a GO library for writing and reading from Excel :   
https://github.com/qax-os/excelize

### A pinch of math

The first shiny thing I wanted was the company's P/E ration.  
I think of it like the companies _hype value_ - the ratio of what people are willing to pay for a company compared to what it actually earned that year.

Let's break it down : 

$$ \text{P/E ratio} = \frac{\text{Price per Share}}{\text{Earnings per Share}}$$

EPS is Net income divided by the number of public shares. (Or all possible shares if were including dilution, in which case it's diluted EPS)

$$ EPS = \frac{\text{Net income}}{\text{Shares outstanding}}$$

### Current results 

I now have a tool that: 

1. Takes my portfolio symbols
2. Fetches their financials
3. Plots them down in excel
4. Calculates P/E ratio for current and previous year, then compares them

![Snapshot of stock Portfolio in excel sheets](/posts/devlog01/stock-sheet-example.png)

Enough to play around with - and a solid base to build on as more ideas come!

Repo : https://github.com/Ziedins/financialReport

### Next updates

* Look if company financials can be sourced somewhere for free (current provider only allows a very limited list of symbols).
* GRAPHS (add one)
* Store historical financials - introduce a DB?

