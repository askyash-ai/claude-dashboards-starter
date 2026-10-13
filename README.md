# Try Claude Dashboards yourself: sample file + prompt

From the reel. Here's everything you need to build the late-orders dashboard yourself in about 5 minutes.

**In this folder**
- `late-orders-sample.csv`: 10 weeks of orders (2,079 rows) for a made-up distributor. Every company, carrier and number in it is fictional.
- This guide, with the exact prompt.

**How to download the file:** tap `late-orders-sample.csv` above, then the download icon (↓) at the top right of the
file. Or use the green **Code** button → **Download ZIP** to get everything at once.

There are two ways to try it. **Option A** works on any Claude plan and takes 5 minutes. **Option B** is the real, live Claude Dashboards, and needs a paid plan and a free Google BigQuery sandbox.

---

## Option A: any Claude plan (5 minutes)

1. Download `late-orders-sample.csv`.
2. Open a new chat at claude.ai and attach the file.
3. Paste this prompt and send it:

```
I've attached late-orders-sample.csv. It's 10 weeks of orders for a made-up distributor.

Build me an interactive dashboard that answers one question: how did late orders in the most recent week compare to the weekly average of the 4 weeks before it, by warehouse?

Rules:
- An order is late when delivered_date is after promised_date.
- Weeks start on Monday and are based on order_date.

Show:
1. Three tiles: late orders this week, the 4-week weekly average, and the % change.
2. A line chart of late orders per week for all 10 weeks.
3. A bar chart of this week's late orders by warehouse.

Under each chart, show how you calculated it (the filter and the formula) so I can check your work. Then tell me in two sentences what's driving the change.
```

Claude builds an interactive dashboard right in the chat. It's a **snapshot** of the file, not a live dashboard: if the data changes, you upload it again. The live version is Option B.

---

## Option B: the real live Claude Dashboards (paid plan)

Claude Dashboards reads from a data warehouse, not an uploaded file. Google's BigQuery sandbox is free (no credit card), so you can put the sample file there and connect Claude to it.

**1. Put the file in BigQuery (about 5 minutes)**
1. Go to `console.cloud.google.com/bigquery` and sign in with a Google account. Create a project if it asks.
2. In the Explorer panel, click the **⋮** next to your project → **Create dataset** → name it `demo` → **Create dataset**.
3. Click the **⋮** next to `demo` → **Create table**.
   - Create table from: **Upload** → pick `late-orders-sample.csv`
   - Table: `late_orders`
   - Schema: tick **Auto detect**
   - **Create table**
4. Sandbox tables delete themselves after 60 days. That's fine for a test.

**2. Connect Claude**
1. In Claude, open **Connectors** and connect **BigQuery**, choosing the project you just made.
   On a company Enterprise account, an owner has to switch Dashboards on first (Organization settings → Artifacts).
2. Start a new chat, choose **Output → Dashboards**, and paste:

```
Using the BigQuery table demo.late_orders, build a dashboard that answers one question: how did late orders in the most recent week compare to the weekly average of the 4 weeks before it, by warehouse?

An order is late when delivered_date is after promised_date. Weeks start on Monday and are based on order_date.

Show three tiles (late orders this week, the 4-week weekly average, the % change), a line chart of late orders per week, and a bar chart of this week's late orders by warehouse. Then tell me what's driving the change.
```

3. Click any number on the dashboard to see the query behind it. Check two things: the **date range** and **what it counted as late**.

---

## Check Claude's work (spoilers)

<details>
<summary>What you should get</summary>

- **Late orders, most recent week (5-11 Oct 2026):** 47
- **4-week weekly average (7 Sep - 4 Oct):** 38
- **Change:** +23.7%
- **By warehouse, this week:** North 19 · South 16 · East 12
- **What's driving it:** 15 of North's 19 late orders went out with **Carrier Bravo**.

If Claude's numbers are different, click the number (or ask "show me the query for that tile") and check the date range and the late rule. That's the habit worth building before you trust any dashboard at work.
</details>

---

## 3 follow-ups to try next

```
Break this week's late orders in North down by carrier.
```
```
Add a filter for customer_segment, and show late orders as a % of all orders, not just a count.
```
```
Which carrier has the worst late rate across all 10 weeks? Show it week by week.
```

## Use it on your own data

Give Claude three things every time, and you'll get a dashboard you can actually use:

1. **The number:** what to count, and the exact rule (e.g. "late = delivered after promised").
2. **The time frame:** which week or month, and when weeks start.
3. **What to compare it to:** last month's average, the same week last year, a target.

Built by @askyash.ai · All data is fictional.
