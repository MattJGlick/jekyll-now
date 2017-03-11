---
layout: post
title: Tax Receipt Project
---

I've been getting more involved with politics since the 2016 Presidential Election and one thing that has really attracted my attention has been the Federal budget.
The US Federal budget is right around 4 trillion dollars. Which is just beating China for the largest budget in the world (~3.5T). The next largest budget comes in with Germany
at around 1.7T. So needless to say I was curious as to where all of this money came from and where all of it goes.

I thought it would be an interesting project to allow someone to enter their income and [filling status](https://en.wikipedia.org/wiki/Filing_status) and then give me a breakdown
of how much they were taxed and where it went. This way the average American would be able to see in real dollar amounts where their tax dollars were being spent. Examining
a large pie graph of the Federal budget can be interesting, but I think that seeing the exact dollar amounts will be more compelling.

It's actually been a good amount of time since I had worked with Angular professionally, so figured it made sense to dive back into it with this project.

## Determining Taxes
The first major task that I needed to complete was to write some functions to determine taxed amounts. I was able to pull the tax 
brackets from [the IRS website](https://www.irs.com/articles/2016-federal-tax-rates-personal-exemptions-and-standard-deductions) for Federal income taxes.

Then I wrote a simple function that takes in the income and filling status and calculates the amount of federal taxable income. That can be seen 
[here](https://github.com/MattJGlick/where_do_my_taxes_go/blob/develop/app/taxes/taxes.service.js) in the taxes service.

Then I also calculated the FICA (basically just Social Security and Medicare) taxes based off [the IRS website](https://www.irs.gov/taxtopics/tc751.html)
Using that information I was able to calculate those taxes as well, which is also seen the in tax service above.

For now, these two sets of taxes are the only ones I plan on focusing on. Obviously state and local taxes would add a whole new layer of complexity that I'm not sure would be useful.
I'm also choosing to entirely ignore deductions, credits, etc. My goal isn't to serve as some sort of Turbo Tax replacement, but just paint a general picture.

So an easy example of this would be a married couple making a $50,000/year would have the following:

Federal Tax: $6572.5

Social Security: $3100

Medicare: $725

Total Liability: $10397.5

## Allocation

The most complicated step that I've yet had to deal with has been weeding through the budget data to determine what makes the most sense to use. Federal income taxes in general aren't
specifically allocated for one specific purpose. That money goes towards mandatory spending (mainly entitlements), discretionary spending and towards interest on loans. To allocate the federal
income tax amounts that I found in the previous section I used Table 4.2 of the 2017 Historical Budget Tables found on [the GPO website](https://www.gpo.gov/fdsys/browse/collection.action?collectionCode=BUDGET&browsePath=Fiscal+Year+2017&searchPath=Fiscal+Year+2017&leafLevelBrowse=false&isCollapsed=false&isOpen=true&packageid=BUDGET-2017-TAB&ycord=534_).

This table gave me a percentage breakdown of each agency and how much their outlays were. I than used those percentages to determine the percentages on the federal income taxes on the user's annual income.

Given the example from above, we could break that liability down into specific agencies, here are some quick examples:

Department of Agriculture: $243.18

Department of Health and Human Services: $2,539.01

National Aeronautics and Space Administration: $32.86

Ideally this could give the average citizen better insight into the exact spending of *their* tax dollars.

## Experimenting with d3 and going forward

Since I have most of the backend handled, the next big step is to make the UI much more user friendly. I've been experimenting with d3 to see the best way to represent the data in a meaningful manner.
I've also considered a bar graph or something or that sort to be able to understand the comparisons from the department. I think long term I'll make up 2 different layouts and then do some basic A/B testing
with some friends and family. Once I've got the layout handled I'll put it up on Heroku for others to use!

_(If you've found any mistakes in my calculations make sure to either add an issue on the repository or shoot me an email)_


