# Instructions for the coding agent

The user is a student learning Dolt (a SQL database with Git-style versioning)
and DoltHub. You run the commands for them in this codespace. Explain briefly
what each command does and show its output, so they learn the workflow.

## Installing Dolt

If `dolt version` fails, install it (the codespace user has passwordless sudo):

```bash
sudo bash -c 'curl -L https://github.com/dolthub/dolt/releases/latest/download/install.sh | bash'
dolt version
```

Before any commit or login, set the user's name and DoltHub email. Ask for
them if you don't have them:

```bash
dolt config --global --add user.name "NAME"
dolt config --global --add user.email "EMAIL"
```

## Logging in to DoltHub

Do NOT run `dolt login`. It waits for the browser and your command will time
out. Instead:

1. Make a new key: `dolt creds new`. It prints a public key.
2. Give the user this link, with the public key at the end, and tell them to
   open it while signed in to DoltHub, type a description such as
   `codespace`, and click **Create**:
   `https://www.dolthub.com/settings/credentials#PUBLIC_KEY`
   If the key is not filled in on that page, tell them to paste the public
   key into it.
3. Wait for the user to say they have done it.
4. Select the key and check it: `dolt creds use PUBLIC_KEY`, then
   `dolt creds check`. It should report the user's DoltHub username. If it
   fails, the key was not added yet: ask them to try the link again.

## Working with a database

- Keep Dolt databases in the home folder (for example `~/retail-orders`),
  not inside this git repository, so they are never committed to git.
- Run SQL with `dolt sql -q "..."`, or load a file with
  `dolt sql < FILE.sql`. Don't open the interactive `dolt sql` shell; it
  waits for input.
- Before committing, show `dolt status` and `dolt diff` so the user sees what
  changed.
- Commit with `dolt add .` and `dolt commit -m "..."`, using a message that
  says what changed.

## Creating a database from a SQL file (retail-orders/)

1. `mkdir ~/retail-orders && cd ~/retail-orders && dolt init`
2. `dolt sql < /path/to/this/repo/retail-orders/retail-orders.sql`
3. Show the tables and row counts, then `dolt add .` and
   `dolt commit -m "Create retail orders database"`.

## Designing a database with the user (sales-csv-data/)

This exercise teaches database design, so the user makes the decisions:

- When asked to design or suggest tables, explain your reasoning and wait.
  Don't create a database or tables until the user says to.
- Build exactly the design the user agreed to. If you think it has a
  problem, say so, but don't change it on your own.
- To load a CSV, you can import it into a temporary table first
  (`dolt table import -c --pk COLUMN TABLE FILE.csv`), fill the real tables
  from it with `INSERT ... SELECT`, then drop the temporary table before
  committing. Import guesses types (money becomes FLOAT), so always fill the
  real tables, with the agreed types, from it.
- When checking that nothing was lost, compare row counts and the actual
  values, and report any differences.
- Show every SQL query you run, so the user can learn from it.

## Analyzing calvinw/BusMgmtBenchmarks (company-analysis/)

The user only reads this database. Clone it with
`dolt clone calvinw/BusMgmtBenchmarks` in the home folder (no login needed),
and never push to it or change it.

Tables:

- `company_info`: one row per company. Primary key `company`. Has
  `display_name`, `ticker_symbol`, `segment`, `subsegment`, `currency`,
  `units`.
- `financials`: one row per company per year. Primary key
  (`company_name`, `year`). Raw amounts: `Net Revenue`, `Cost of Goods`,
  `Gross Margin`, `SGA`, `Operating Profit`, `Net Profit`, `Inventory`,
  `Current Assets`, `Total Assets`, `Current Liabilities`, `Liabilities`,
  `Total Shareholder Equity`, ...
- `financial_metrics`: one row per company per year, same key. Ratios that
  are already computed: `Gross_Margin_Percentage`, `SGA_Percentage`,
  `Operating_Profit_Margin_Percentage`, `Net_Profit_Margin_Percentage`,
  `Inventory_Turnover`, `Asset_Turnover`, `Return_on_Assets`,
  `Current_Ratio`, `Quick_Ratio`, `Debt_to_Equity`,
  `Three_Year_Revenue_CAGR`, `Sales_Current_Year_vs_LY`.
- `segment_metrics`, `subsegment_metrics`: benchmark averages by segment.
- Views such as `company_comparison_2024_view` join these for one year.

Join `financials` and `financial_metrics` to `company_info` with
`company_name = company`.

Things to get right:

- Column names in `financials` contain spaces: quote them with backticks,
  for example `` `Net Revenue` ``.
- Amounts are in **thousands** of the company's own currency (`units` and
  `currency` in `company_info`). 4948587 means about 4.95 billion. Most are
  USD, but some are GBP, EUR, CAD or SEK. Don't compare raw amounts across
  currencies; compare percentages and ratios, or say clearly that the
  currencies differ.
- Percentages are already in percent (62.27 means 62.27%).
- `year` is the fiscal year. `reportDate` is when that fiscal year ended,
  which for many retailers is early the next calendar year.
- Use the ratios in `financial_metrics` rather than recomputing them, and if
  you do compute something yourself, say so.
- To get data into Python, run
  `dolt sql -r csv -q "SELECT ..." > file.csv` inside the database folder and
  read the CSV with pandas.
- Install whatever you need for charts and slides (for example Python with
  pandas, matplotlib and python-pptx). Save charts as PNG files. Keep the script you used in the report
  folder so the work can be rerun.
- In slides, keep text short and check that it fits; put one chart per
  slide, large enough to read.
- Every number in the analysis and slides must come from a query you ran.
  Show the SQL.

## Pushing to DoltHub

- `dolt push` cannot create a database on DoltHub. The user first creates an
  empty database on the DoltHub website. If they haven't, tell them to do
  that, then wait.
- Push only to the user's own DoltHub account, never to `calvinw/...`:
  `dolt remote add origin USERNAME/DATABASE-NAME`, then
  `dolt push -u origin main` the first time and `dolt push` after that.
- If the push says permission denied, the login is missing or the database
  belongs to someone else: check `dolt creds check` and the remote with
  `dolt remote -v`.
- After pushing, tell the user to refresh their database page on DoltHub.
- Don't use `--force`, don't delete tables or branches, and don't rewrite
  history unless the user asks.
