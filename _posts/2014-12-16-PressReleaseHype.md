---
layout: post
title: Identifying exaggerated press releases from public data
---

We now know that scientific press releases often exaggerate. But can we identify the worst offenders?

A <a href="http://www.bmj.com/content/349/bmj.g7015">recent paper</a> by Sumner et al. in the BMJ analysed 462 press releases associated with scientific papers related to health research published by 20 leading UK universities in 2011. They found that, when compared to the original journal article,
<ul>
	<li>"40% of the analysed press releases contained more direct or explicit advice"</li>
	<li>"33% of primary claims in press releases were more strongly deterministic"</li>
	<li>"For studies on animals, cells, or simulations, 36% of press releases exhibited inflated inference to humans"</li>
</ul>
These are sobering statistics. It's long been the fashionable thing for scientists to blame journalists for the misrepresentation of their work. Sumner et al. have shown that for the papers they analysed exaggeration of various kinds at the press release stage is not uncommon. This should be where authors theoretically have some control, so it's particularly embarrassing.

Sumner et al. focused on summary statistics about the overall problem. However, as Ben Goldacre (<a href="https://twitter.com/bengoldacre">@bengoldacre</a>) pointed out in a <a href="http://www.bmj.com/content/349/bmj.g7465">linked editorial</a>, it would be possible to use the published data to find "those academics and institutions associated with the worst exaggerations and publish their names online, along with details of the transgressions" (<a href="http://www.bmj.com/content/349/bmj.g7465">source</a>).

I liked the idea of extracting the information so that individual press releases could be analysed easily, so I downloaded the data.

[Aside: I was disappointed to find that the data files were all in the proprietary MATLAB (.mat) format. I'm not sure why the authors chose to release the data like this given that an individual license for MATLAB costs <a href="http://uk.mathworks.com/pricing-licensing/index.html?intendeduse=comm">£1600</a>. Fortunately I have access to MATLAB through my university, but I think journals should be much more active in encouraging the release of supplementary material in non-proprietary formats.]

<b>Data extraction details</b>

In extracting the data for individual press releases, I chose to stick fairly closely to the criteria used by Sumner et al. for simplicity. Each journal article, press release, and related news article included in the study was coded according to a set of guidelines detailed in their <a href="http://figshare.com/articles/InSciOut/903704">supplementary material</a>. I read these guidelines and then tried to link them to the variables present in the final dataset to extract the information of interest for every press release. This wasn't especially trivial and I may well have made mistakes in this step - the code is available on <a href="https://github.com/liampshaw/pr_hype">GitHub</a> for checking. I'm not a MATLAB user normally, so it's very rough and ready.

I chose to restrict the analysis to press releases and to stick fairly closely to the data used for summary statistics by Sumner et al. The information I aimed to extract was:
<ul>
	<li>The reference number given to the paper and press release by Sumner et al.</li>
	<li>The titles of the paper and press release</li>
	<li>The authors of the original paper (using a PubMed search by title)</li>
	<li>The university the press release was issued by</li>
	<li>The study sample, as reported in the paper and in the press release (to identify e.g. inference to humans from animal research)</li>
	<li> The strength of any advice given in the paper and in the press release (to identify e.g. exaggeration of advice given to readers)</li>
	<li>The strength of causation according to the paper and to the press release (to identify e.g. exaggeration of correlative statements into causative statements)</li>
	<li>The main variables in the study according to the paper and to the press release (to identify e.g. generalization of variables)</li>
	<li>Whether the word "cure" was used</li>
</ul>
<strong>Results</strong>

The resulting csv file is available on <a href="https://github.com/liampshaw/pr_hype">GitHub</a> or as a <a href="https://docs.google.com/spreadsheets/d/18Qmhy6puIBDKqOezt15W7gXCmQ3QGoxdvqueoP4Aqys/edit?usp=sharing">Google Spreadsheet</a>.

I invite anybody who's interested to take a look and do their own analysis. <del>There are some missing entries in the author data (69/462) due to problems with the PubMed lookup, even for some papers that are present on PubMed - I'm not sure why this is and will try to fix it</del> (EDIT: the code has been updated and now only 18 papers lack authors because they aren't indexed on PubMed. That indicates that they're not typical health research papers - sure enough, looking at the titles most are of a more sociological flavour - but I plan to add them manually for completeness when I get a chance). The authors seem to be accurate based on manually checking a small random sample of the data - see for yourself by going to the PubMed URL provided. For other variables, all missing entries (often coded as '-9') are as present in the original data files.

In that spreadsheet it should be possible to sort the publications by a variable and quickly identify papers and authors that were coded as such. You can then look at the <a href="http://figshare.com/articles/InSciOut/903704">original data</a> and use the reference number to read the press release (in folder '5. Press releases')  to see if you agree with the assessment of Sumner et al.

For example, let's look at some in which the study sample was generalized in a major way when written about in the press release. This corresponds to a value of 2 in the 'Sample_changed' column. There are 85 press releases which meet this criteria, and you can see what the samples were in the 'Sample_journal' and 'Sample_PR' columns.

Or take the exaggeration of advice. A value of 3 in the 'Advice_exaggeration' column corresponds to explicit advice to the general public present in the press release when the paper contained no advice. There are 19 papers that meet this criteria. I've left the Google spreadsheet sorted in this order.

I plan to do some more analysis myself, but please feel free to use the data yourself, bearing in mind some caveats...

<b>Preliminary thoughts</b>

The spreadsheet I've provided simply represents my attempt at extracting a summary of what Sumner et al. have already publicly released. I would recommend caution before accusing authors of misrepresentation based solely on the information here, both because I may have extracted the data incorrectly and because that data itself comes from subjective judgements (although the coding guidelines are rigorous and Sumner et al. showed a high concordance of 91% between blinded coders).

Even if the information is accurate, much stronger evidence would be required to suggest that anybody identified here as an author of a paper that had an exaggerated press release was being duplicitous or deliberately misleading. I think the gradual exaggeration of what might have been a measured scientific article can happen when scientists and universities are trying hard to sell their research as relevant to the general public. Sumner told James Hamblin at <em>The Atlantic </em>that correlative statements in papers ("significant associations between variable x and outcome y") often become causative statements in press releases ("variable x increases risk of outcome y"):

"It is very common for this type of thing to happen...probably partly because the causal phrases are shorter and just sound better. There may be no intention to change the meaning." (<a href="http://www.theatlantic.com/health/archive/2014/12/as-academia-melts/383570/2/">source</a>)

This is a bad situation, but by acknowleding the problem the academic community can begin to tackle it. As Goldacre points out, this should require only "a modest extension of current norms". (<a href="http://www.bmj.com/content/349/bmj.g7465">source</a>)

Scientists have a responsibility to avoid exaggerations in press releases for their papers instead of passing the buck to journalists (<a href="http://www.telegraph.co.uk/health/healthnews/11290053/Why-scientists-not-journalists-are-bad-for-your-health.html">some</a> of <a href="http://www.independent.co.uk/news/science/bad-science-reporting-blamed-on-exaggerations-in-university-press-releases-9913336.html">whom</a> have already used this paper as an opportunity to pass the buck right back, which isn't very helpful). A culture of calling out and attempting to prevent these sorts of exaggerations at every level - in news articles, in the press release, and also in the original paper - would be a good thing. It certainly seems reasonable to me that academics are made accountable for their own press releases as Goldacre recommends.

As to how those press releases should best be written: Sumner et al. are apparently following up this retrospective study with a randomised trial looking at "how different styles of press releases, and variants in specific phrasing, influence the accuracy and quantity of science news" (<a href="http://www.theguardian.com/science/blog/2014/dec/10/science-health-news-hype-press-releases-universities">source</a>).

<b>Get the data:</b>

Data extracted: available as a <a href="https://docs.google.com/spreadsheets/d/18Qmhy6puIBDKqOezt15W7gXCmQ3QGoxdvqueoP4Aqys/edit?usp=sharing">Google spreadsheet</a> or from <a href="https://github.com/liampshaw/pr_hype">GitHub</a>

Code: available via <a href="https://github.com/liampshaw/pr_hype">GitHub</a>

<strong>Resources:</strong>

Original article: Sumner et al., <a href="http://www.bmj.com/content/349/bmj.g7015">'The association between exaggeration in health related science news and academic press releases: retrospective observational study'</a>, <em>BMJ </em>2014;349:g7015

Original data and supplementary material: <a href="http://figshare.com/articles/InSciOut/903704">here</a>
