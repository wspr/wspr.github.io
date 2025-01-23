---
layout: post
title:  "Finance plans and finance apps — mainly Up and Stake — in 2025"
date:   2025-01-23
categories: finance
---

After a few years dabbling in minor share purchases and slightly less minor ETF purchases as a way to build an investment portfolio, I realised that the [all-in-one VDHG ETF](https://passiveinvestingaustralia.com/vdhg-or-roll-your-own/) was the best option for me. Vanguard are the professionals and there’s no point trying to reinvent their wheel.

So in late 2023 I started a fairly simple but effective system, splitting my fortnightly income into buckets of spending, saving, and investing. I use Up Bank, which makes automatic pay splitting like this really streamlined. (More thoughts on the Up app later.) Once enough money had accumulated in the investment bucket, I transferred it over to BankSA DirectShares, my shares platform until recently.

Why not just buy shares every pay cycle? Well, sometimes I did. But DirectShares charges $20 per shares transaction, so spending even small single digits’ percentage of the worth of the purchase seems significant when you might only see 5% or so growth in a mediocre year. Keeping the money in a bank account accruing interest for a while increases the benefit of a waiting. In fact, choosing an optimal purchasing frequency is an interesting optimisation problem — solved by the fantastic “[Investment Frequency Calculator](https://investcalc.github.io)”.

Regardless of how well timed my purchases could have been, I was spending a few hundred dollars on brokerage fees with DirectShares. Furthermore, although the interface was actually quite functional when trawling back through records of purchases and sales, I always found the website and app to be reasonably clunky at the best of times, and busy and full of irrelevant cruft at others. After using the phone-only Up Bank interface, which is a true first class citizen on my phone (supporting Apple Wallet, naturally, but also other iOS interface features such as widgets), I slowly started to yearn for an equivalent experience when buying shares.

Which brings me to Stake. I heard about this from lurking in various Australian finance subreddits. It ticked all the boxes: cheap brokerage (only $3!), native app, CHESS sponsored, with the added bonus that it can handle US shares (my first very modest shares purchase was AAPL and I’m holding onto it for sentimental reasons). Nonetheless, shifting brokers is no walk in the park. There is annoying paperwork associated with shifting your shares from one broker to another. It took me a while to build up the courage to go through with it.

I was very pleased to discover that the process of brokerage transfer through Stake is almost as frictionless as one could imagine. They’ve really designed a worthwhile system. Stake makes it almost trivial to designate which broker I’m transferring from, provide the appropriate paperwork for ID checks, and indicate which funds to transfer across. But it’s not an instant process. It took a couple days to bounce the information from Stake to DirectShares, then I had to call DirectShares as one last security check (appreciated!), after which it took another couple days to finalise the transfer. Although this sounds lengthy, I found it a very seamless and trustworthy process.

Stake currently offer one full year of 100% brokerage discount to transfer an existing portfolio to them, so I can now buy shares as often as I like. Even after the year is up, spending $3 instead of $20 dramatically changes the equation and I suspect I’ll be able to continue purchasing shares fortnightly. The benefit of this, I believe, is the greatest chance of averaging out short term fluctuations. 26 purchases across the year minimises the chance I’ll accidentally buy in a significant dip — or more likely, minimises the chance that I’ll think too much at all about trying to time the market.

Saving a few hundred on brokerage fees also got me thinking about interest rates. Up at time of writing offers 4.35%. This is good, but not great — the best rate on the market is 5.5%, albeit with some different terms and conditions how you achieve them respectively. (Interest rates can be compared via incredible resource provided by the “[Accounts Leaderbook](https://www.accountsleaderboard.au/)” online spreadsheet.)

So despite wanting to keep my finance life as simple as possible, a 1.15% increase by moving my liquid savings (emergency fund) into a new bank account was worthwhile purely from a numbers perspective. I signed up for UBank and (a) it was super easy, (b) it’s really surprising how different it is to the Up app. In terms of [user interface playgrounds](https://daringfireball.net/2009/04/twitter_clients_playground), online banking might be very fertile ground. (This seemed more surprising to me than the marked differences between the DirectShares app and the Stake app, since those two are so vastly different in provenance that a comparison is hardly worthwhile.)

Recapping, heading into 2025 I’m now feeling good that:

* I have a simple investment strategy that I can manage without much brainpower and won’t get distracted “tweaking” by introducing more diversification or adjusting splits. 
* I’m getting the best bang for the buck in brokerage fees and using a nice app to do so.
* I’m earning as much interest as possible on my emergency fund.

There is one loose end around super concessional contributions, but that’s too annoying to try to discuss now for various boring reasons.

Finally, I’ve realised that I’ve been relying more and more on phone interfaces for finance matters. My phone is never far away, and is fast and easy. With apps well designed for the platform it feels an order of magnitude more productive (to me) than sitting down in front of a full-size computer, pulling up the websites, logging in, etc. (These are also the reasons why I’m terrible at using my digital cameras even though I have a couple that I really like to use.)

To further this phone-first approach (actually phone-only, considering some of these platforms don’t even have websites), I have been building a process to record my finances in a CSV file and visualise them using Python and Matplotlib. (Respectively using [Easy CSV Editor](https://vdt-labs.com/easy-csv-editor-mobile/) and [Pythonista](https://omz-software.com/pythonista/).) I’m not quite ready to talk about this code and what it can do but I’m calling it “[Net Worth Dashboard](https://github.com/wspr/networthdash)”.

What is funny about this after all the thinking and building of these processes, this scheme, sensibly, should now just require long stretches of patience as the payslips come in, the brokerage orders go out, and the portfolio creeps steadily upwards. You know, unless the world crumbles into unmitigated disaster for all sorts of highly conceivable reasons in the next few years. 