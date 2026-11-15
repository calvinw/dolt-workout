# Analyze Retail Companies with an Agent

This time you don't build a database. You analyze one that already exists:
[calvinw/BusMgmtBenchmarks](https://www.dolthub.com/repositories/calvinw/BusMgmtBenchmarks)
on DoltHub. It holds financial results for about 60 retail companies (Gap,
Nike, Macy's, TJ Maxx, Zara and many more) for the years 2018 to 2025, taken
from their annual reports.

You pick **two companies** and **two years**. The agent studies the database,
compares the two companies in each year with charts, and turns its analysis
into a PowerPoint deck.

## Before you start

1. Start a codespace on your copy of this repo, run `opencode`, and connect
   OpenRouter (see the main README).
2. If Dolt isn't installed in this codespace yet, paste this first:

   ```default
   Install Dolt and set it up with my name YOUR NAME and my email YOUR EMAIL.
   ```

You don't need to log in to DoltHub: you only read this database, you don't
push to it.

Copy each prompt into OpenCode and press **Enter**. Read what the agent says
before you go on. If it asks to run a command or install something, allow it.

## Step 1: Get the Database

```default
Clone the Dolt database calvinw/BusMgmtBenchmarks into my home folder.
```

## Step 2: Understand the Database

```default
Describe the BusMgmtBenchmarks database. For each table, tell me what one row represents, what its columns mean, and its primary key. Explain how the tables connect, what the views are for, and how many companies and years it covers.
```

```default
What units and currencies are the dollar amounts in? What does the year column mean, and how is it different from reportDate?
```

```default
List all the companies, grouped by segment and subsegment.
```

## Step 3: Pick Two Companies and Two Years

Pick two companies that are fair to compare, for example two from the same
segment (Gap and American Eagle, Macy's and Nordstrom, TJ Maxx and Ross).
Pick two years at least two years apart. Then check that the data is there:

```default
Do COMPANY A and COMPANY B both have data for YEAR 1 and YEAR 2? Show me their Net Revenue for those years, and tell me what currency each one reports in.
```

If one is missing a year, pick a different year.

## Step 4: Compare Them

```default
For COMPANY A and COMPANY B, compare them side by side in YEAR 1, then side by side in YEAR 2. Use the financials and financial_metrics tables: revenue, gross margin %, operating profit margin %, net profit margin %, SG&A %, inventory turnover, current ratio, return on assets and debt to equity. Show the SQL you ran and put the results in small tables.
```

```default
Explain what these numbers say about how each company makes money. Which one is more profitable, and why? Which one manages its inventory better? What changed for each company between YEAR 1 and YEAR 2?
```

## Step 5: Make Charts

```default
Create a folder called company-analysis/report/charts. Make clear charts that compare COMPANY A and COMPANY B in YEAR 1 and YEAR 2, and save each one there as a PNG file. Include at least: net revenue, the profit margins (gross, operating and net), SG&A %, inventory turnover, and return on assets. Give every chart a title, labeled axes, and a legend.
```

Open the `charts` folder on the left and click each picture to look at it.
If a chart is hard to read, tell the agent what to fix.

## Step 6: Write the Analysis

```default
Write your full comparison of COMPANY A and COMPANY B into company-analysis/report/analysis.md. Back up every finding with numbers from the database, and say which year each number is from.
```

## Step 7: Build the Slide Deck

```default
Create a PowerPoint file called company-analysis/report/company_comparison.pptx with 8 to 12 slides: a title slide, a slide about the two companies (segment, what they sell, currency), a slide comparing them in YEAR 1, a slide comparing them in YEAR 2, slides with the most important charts and what each one shows, a slide of key findings, and a final slide on which company looks stronger and why. Keep the text on each slide short.
```

Click `company_comparison.pptx` in the file list to open it in the codespace,
and look through every slide. If text runs off a slide, a chart is missing,
or a number doesn't match the analysis, tell the agent what to fix.

## Step 8: Check the Agent's Work

Pick one number from the slides and ask the agent to prove it:

```default
Show me the exact SQL query that gives COMPANY A's gross margin % in YEAR 1, run it, and check that it matches the slide.
```

## Step 9: Save Your Work

```default
Commit the company-analysis/report folder to git and push it to GitHub.
```

## What to Hand In

The link to your GitHub repository, with `company-analysis/report/` holding
your charts, `analysis.md` and `company_comparison.pptx`.
