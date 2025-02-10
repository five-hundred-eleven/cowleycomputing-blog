---
title: 'Finish Types in the UFC'
description: "   This is my Unit 1 project for Lambda School. The goal of this project was to identify interesting trends in MMA by exploring publicly available UFC data.  Research Question -----------------  For each of a few countries with high UFC participation, plot..."
date: '2019-11-17'
---


This is my Unit 1 project for Lambda School. The goal of this project was to identify interesting trends in MMA by exploring publicly available UFC data.

Research Question
-----------------

For each of a few countries with high UFC participation, plot the proportion of wins to total number of fights by year. "Wins" are further broken down into Decisions, TKOs, and Submissions.

Which countries have high UFC participation?
--------------------------------------------

The first part of our question requires us to find countries of interest i.e. countries with high UFC participation. There are potentially several metrics we could use:

1. Countries in which the greatest total number of UFC fighters were born
2. Countries in which the greatest per capita number of UFC fighters were born
3. Countries which are hosting the greatest total number of fighters
4. Countries which are hosting the greatest per capita number of fighters

Options one and two were eliminated because data was unavailable. Option three is skewed in favor of high population countries. Four was the best option.

The following plots were made using Sherdog's UFC datasets (linked at the bottom of the page).

We see that the highest per capita participation is in the U.S., Brazil, and Canada. Iceland and Ireland (low population countries) also have a high per capita participation. It is difficult to see the difference between medium-to-low participation countries. For this reason, we will make another graph with high-participation countries omitted.

There are medium levels of participation in England, Sweden, Russia, Australia, and Poland. Our final list of countries will be the U.S., Brazil, Canada, Russia, Poland, and Japan.

Which outcomes are common among fighters from each country?
-----------------------------------------------------------

Here are the percentages of fights won by **decision** (split or unanimous), **submission**, or **knockout** (KO or TKO). The **total wins** are also displayed. Losses and disqualifications are not shown. The percentages are out of the total number of fights fought by athletes from the given country.

#### Brazil

Early on the chart we see 100% of fights were won by submission (Joyce Gracie). The ratios even out as time goes on. Interestingly in 2018 we see more wins by TKOs than Decisions for the first time since 2008. Notable Brazilian athletes that achieved TKOs in 2018 include Amanda Nunes.

#### USA

American fighters lost the majority of their early fights, with most wins coming from submission (Ken Shamrock). The stats fluctuate significantly through the 2000s. Since 2009, the numbers have been fairly constant, with most fights won by decision, then TKO, and lastly submission.

#### Japan

Japan won 1 fight by submission in 1997 (Kazushi Sakuraba). Japan's participation in the UFC has been low which causes the numbers to fluctuate.

#### Russia

Russia has become more prevalent in recent years, winning a large majority of their fights in 2017 and 2018. In 2018 Russia won more fights by submission than by TKO (Khabib Nurmagomedov, Islam Makhachev).

#### Canada

Canada had a high percentage of TKOs early on. Since 2009 most wins have been by decision.

#### Poland

Polish athletes achieved many TKOs from 2005 to 2013. Since 2014 most wins were by decision.

#### All Countries

This plot shows the UFC as a whole. In the 1990s, Submissions were most common. In the 2000s, KOs/TKOs were frequent. Since 2009 most wins have been by decision.

Conclusions
-----------

Some of the trends are clearly due to rule changes in the UFC. For example early fights had no time limit so there were no wins by decision. In the past decade by far most UFC fights ended in decision.

#### Which country is dominant?

Brazil has always had a high percentage of wins, but in recent years Russian athletes have been the most dominant.

Resources
---------

* [Notebook](https://github.com/five-hundred-eleven/DS-Unit-1-Build/blob/master/ipynb/explore_data.ipynb)
* [Fight Data from Kaggle](https://www.kaggle.com/rajeevw/ufcdata)
* [Fighter Data from Sherdog](https://docs.google.com/spreadsheets/d/1z3QX0uWXv-XHX2Nfuj6zZHrfEeXI3A9CKWkrGaBzB8s/edit#gid=0)

