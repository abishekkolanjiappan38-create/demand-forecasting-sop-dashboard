# Demand Forecasting & S&OP Dashboard

I built this project to dig into a question that comes up constantly in supply chain roles: how do you actually know if your forecast is any good, and are the problems you see in your data the real problems, or just the obvious ones?

Using the DataCo Smart Supply Chain dataset (180,519 orders from a global retailer, Jan 2015–Sep 2017), I built a full Power BI dashboard from the ground up — custom data model, 20+ DAX measures, and a baseline forecasting model — to answer three things: how accurate is the demand forecast, where is money actually being lost in delivery, and what's really driving sales trends over time.

## What I found

The forecast model (a 3-month rolling average, used as a defensible baseline) came out with a **MAPE of 5.53%** — solidly under the 10% mark that's generally considered good in retail forecasting.

The more interesting finding was on delivery. At first glance, a **54.41% late delivery rate** looks like a serious operational problem. But when I broke it down by region, it showed up almost identically everywhere — 48% to 56% across all 23 regions, with no clear worst offender. Combined with the fact that the actual delay was only about half a day on average, that told a different story: this isn't a logistics failure happening in specific places, it's a **scheduling/promise-setting problem** baked into how delivery windows are set company-wide. That's a much cheaper problem to fix than an operations overhaul.

## How it's built

I set this up with a proper star schema rather than working off the flat dataset directly — a custom date dimension table connects to the main order data, which is what makes reliable month-over-month and year-over-year calculations possible in the first place. Getting that relationship working correctly involved catching a data type mismatch between the two date fields, which was a good reminder that data modeling bugs don't always throw errors — sometimes they just quietly give you wrong numbers until you go looking.

From there, I wrote out 20+ DAX measures covering everything from basic totals to a rolling forecast model and a MAPE calculation that deliberately excludes the first few months, since there's no way to forecast against data that doesn't exist yet.

## The dashboard itself

Four pages, each answering a different piece of the puzzle:

- **Executive Summary** — the 30-second version: top KPIs, sales trend, category and regional splits
- **Forecast vs. Actual** — how close the model actually got, month by month
- **Sales Trend & Growth** — momentum over time, not just totals
- **Delivery & Fulfillment** — where the late-delivery story lives

## What's in this repo

- `Powerbi_Project_Supply_chain_data_co.pbix` — the full interactive dashboard, open it in Power BI Desktop to explore
- `Data_co_supply_chain_project_dataset_report.pdf` — the written project report

## Dataset

[DataCo Smart Supply Chain Dataset](://https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis) via Kaggle

---

Abishek Kolanjiappan — OSCM & Marketing, University of Toledo
