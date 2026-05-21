# Facebook Attribution Window Optimization

**28%.** That is the average drop in reported [ROAS](/resources/facebook-roas-improvement-guide-from-black-box-to-profit-engine) when you strip view-through conversions out of a Meta campaign and look at click-driven results only. I have run that test on dozens of accounts. The number is remarkably consistent, and it is remarkably uncomfortable, because it means a big chunk of the ROAS most advertisers report to their boss is attribution, not revenue.

I have managed Meta spend through every attribution-window regime since the iOS 14 reset. I have watched the same campaign report a 4.1 ROAS on 7-day click plus 1-day view and a 2.9 on 1-day click only. Same campaign.

Same week. Same actual sales. **The window just decided how generous the story was allowed to be.**

This is not another "which window should I pick" post. There are a hundred of those, and they all argue about reporting accuracy as if the only thing at stake is your dashboard. The dashboard is the small problem.

Here is the part those guides skip: the attribution window is not a reporting setting. It is a model-training setting. The window you choose decides what counts as a conversion, and what counts as a conversion is exactly what Meta's bidding algorithm learns from. **Pick a loose window and you are not just inflating a report.

You are teaching the machine that spends your money to chase the wrong people.**

The fix is not picking a magic window. The fix is controlling what conversion signal leaves your site in the first place: first-party, filtered, with the junk stripped before it reaches Meta. That is the architectural piece DataCops handles.

See the [Meta Conversion API](/meta-conversion-api), [fraud traffic validation](/fraud-traffic-validation), and our [Facebook attribution settings deep-dive](/resources/facebook-attribution-settings-optimization-the-algorithms-secret-lever).

## Quick stuff people keep asking

**What is the best Facebook attribution window setting?** For reporting honesty, 7-day click. For training the algorithm on real intent, 7-day click is also the safest default. View-through is where the inflation lives.

There is no single "best" - but there is a "least misleading," and that is click-based.

**What does 7-day click 1-day view mean in Meta Ads?** It credits a conversion to your ad if the person clicked within 7 days before buying, OR merely saw the ad within 1 day before buying. The "saw it" half is view-through. They never interacted.

Meta still claims the sale.

**Does Facebook attribution inflate ROAS?** Yes, structurally. View-through conversions are typically 15 to **35%** of Meta-attributed conversions. Most of those buyers would have converted anyway.

Counting them as ad-driven inflates ROAS by roughly **28%** on average in my testing.

**How do I compare attribution windows in Meta Ads Manager?** Use the comparison feature in the columns menu - it shows the same campaign under multiple windows side by side without changing your optimization setting. Run 7-day click against 7-day click plus 1-day view. The gap between those two columns is your inflation, quantified.

**What is view-through attribution on Facebook?** Credit given for an impression with no click. The person scrolled past your ad and bought something later. Meta treats the scroll-past as causal. Sometimes it is. Often it is not.

**Why does my Facebook ROAS not match my actual revenue?** Because Meta counts conversions its window allows, deduplicates differently than [GA4](/alternative/ga4-alternative), and includes view-through. GA4 is last-click and stricter. Your bank statement is truth.

Meta is the most generous narrator in your stack.

**How does attribution window choice affect campaign optimization?** This is the real question. Meta optimizes toward whatever it is allowed to call a conversion. A loose window labels more events as conversions, so the algorithm learns from a wider, noisier, partly-fabricated set of "wins" and targets accordingly.

**What is engaged-view attribution in Meta Ads?** Credit for a video view of a certain minimum duration without a click. A softer cousin of view-through. Still an impression-based signal, still a weaker proxy for intent than a click.

## The window is a training signal, not a report setting

Here is the chain nobody draws for you.

You pick 7-day click plus 1-day view. Meta now records every in-window purchase as a conversion and feeds those conversions back into its own bidding model as positive examples. The model studies them: which audiences, placements, creatives, times of day produced these "wins." Then it spends your next dollar chasing more of the same.

Now remember that 15 to **35%** of those wins were view-through. People who scrolled past an ad and bought anyway. They were going to buy regardless.

But the algorithm cannot tell a caused conversion from a coincidental one. It just sees "conversion, credited to this ad set" and learns from it.

So the model learns from a conversion set that is one-fifth to one-third noise. It optimizes toward the audiences that generate lots of cheap impressions near people already about to buy - retargeting pools, your own warm audiences, brand-name searchers. It looks brilliant in the dashboard because those people convert.

They were always going to. You are paying Meta to take credit for your existing demand, and Meta's model is getting better and better at finding more of that easy credit instead of finding you new customers.

This is Layer 5 of how ad data quietly rots. Inflated, partially fabricated conversion signal goes into the platform. The platform trains on it.

The platform optimizes toward the [segment](/alternative/segment-alternative) that produces the most attributable-but-not-incremental conversions. Real new-customer acquisition gets starved because, to the algorithm, it looks less efficient. ROAS on the dashboard stays high or even climbs.

Actual business growth flattens. Garbage signal in, confident-looking garbage out.

And it compounds. Week one, the model leans slightly toward easy retargeting wins. Week four, it is heavily weighted there because every loop reinforced it.

Week twelve, your "best" campaign is a near-pure brand-defense play wearing a prospecting campaign's name, and the window you picked in the settings panel six months ago is why.

Now stack a second problem on top, because in 2026 you have to. Some meaningful share of the impressions and clicks Meta is counting are not human. Bots and automated agents generate impressions and clicks.

When a bot's path happens to land inside your view-through window, that is a fabricated conversion sitting in your training set. You are not just teaching the model to chase your existing customers. You are partly teaching it to chase non-humans.

It cannot tell the difference, because nobody filtered the signal before it arrived.

That last sentence is the actual root cause. Not the window. The window only decides how wide a net you cast over an unfiltered stream.

The deeper problem is that the conversion signal leaving your site was never cleaned. The Meta pixel is a third-party script. It fires on whatever the browser hands it - real buyers, bot sessions, scroll-past impressions - with no isolation and no verification before that data leaves your infrastructure and becomes Meta's training material.

Tighten the window all you want. You are still feeding the model from a dirty pipe.

## What to actually do

**Run the comparison report before you touch anything.** Columns menu, compare 7-day click against 7-day click plus 1-day view. Write down the gap. That percentage is your view-through inflation.

Now you are arguing with a number instead of a vibe.

**Default to 7-day click for prospecting.** You want the algorithm learning from people who took a deliberate action. Clicks are a far better intent proxy than impressions. Cleaner signal in, better targeting out.

**Be honest that view-through has a use - a narrow one.** For top-of-funnel awareness video, view-through tells you something real about reach effect. Just never let it drive the optimization of a campaign whose job is measurable acquisition. Report it.

Do not optimize on it.

**Reconcile to the bank, monthly.** Meta's number, GA4's number, your actual deposited revenue. The Meta-to-bank gap is your true attribution tax. Track it as a trend. If it widens, your window is getting more generous than your business.

**Filter the conversion signal before it leaves your site.** This is the structural fix. Instead of letting the raw pixel ship every browser event straight to Meta, route conversions through a first-party pipeline on your own subdomain that strips bot and invalid traffic at ingestion, then sends one clean, verified conversion stream to Meta via CAPI. Now the window setting governs a clean stream.

The model trains on real humans who really converted. That is the DataCops approach - and it is also far more resilient to ad blockers than the browser pixel, so you stop losing the legitimate clicks at the same time.

## Decision guide

Prospecting campaign, cold audiences? 7-day click only. Make the algorithm earn its conclusions from real clicks.

Retargeting warm audiences? 7-day click plus 1-day view is defensible - but know that ROAS is partly attribution theater, and judge the campaign on incremental lift, not the headline number.

Long consideration cycle, high price point? 7-day click, and pair it with a holdout or geo lift test, because no window captures a 30-day decision honestly.

Lead generation, not ecommerce? 7-day click. View-through credit on a free lead form is almost pure noise and will pull the model toward junk leads.

Boss wants the ROAS number to look good? That is the trap. The window that flatters the report is the window that quietly misdirects the spend. Pick the honest window and explain the gap once.

Already optimized on a loose window for months? Switch to click-based, expect a relearning dip, and feed it clean filtered data while it recovers. The model has to be re-taught. There is no instant reset.

## You did not pick a setting. You picked a teacher.

The mistake I see constantly: people treat the attribution window as a reporting preference, something you tune so the dashboard tells a nicer story to leadership. It is not that. It is the definition of "success" you handed to the algorithm that spends your budget.

Loosen it and you have not improved performance. You have just lowered the bar for what counts as a win, and the machine will happily clear a lower bar all day with your money.

Reported ROAS is not a fact about your business. It is a function of a window you chose and a conversion stream nobody filtered.

So go pull the comparison report. Find your view-through percentage. Then ask the harder question: of the conversions Meta has been training on for the last six months, how many were real humans your ads actually caused to buy - and how many were scroll-pasts, existing customers, and bots that your window was generous enough to count?

Until you know that number, you do not know what your campaigns are really doing. You only know what the most generous narrator in your stack chose to tell you.

---

Research by [DataCops](https://www.joindatacops.com) — first-party tracking, consent infrastructure, fraud prevention, and server-side CAPI for Meta, Google, TikTok, and LinkedIn.
