# Project Log & Prometheus Notes

## Progress Log

So far, we've gained the fundamental knowledge of what the tools are and how to use them. Now we actually have to start building the thing — so we have to host something on the cloud and develop it. We have to start somewhere, because only then can we move on to the future process and stuff.

The thing is, I have to handle the connection part myself. That's technically my teammate's job, but I know he won't do it until the very last moment before the submission deadline, so I'll do it myself for now.

Before that hands-on work, I was thinking of first reading a bit about **Prometheus** — the sensor we'll be deploying on the pod that will give us continuous reports on what's right and what's wrong. So let's proceed: first we'll learn what exactly Prometheus is and what data it gives.

Then, before the full hands-on setup, we'll locally run a pod and set up Prometheus on it, to see what it actually gives us before we set it up on the main machine/server.

![Prometheus architecture reference](https://github.com/user-attachments/assets/200bc3b4-bf26-4210-99cb-f3c25036eb78)

---

## What Is Prometheus?

At its core, **Prometheus is an incredibly fast, specialized database designed specifically to store numbers that change over time** (time-series data).

Think of it as a hospital monitor for your infrastructure. It continuously checks the "vitals" (CPU, memory, error rates) of your applications, stores that history, and sounds the alarm if something looks sick. For a system like Aegis, this is what allows your automated triage pipeline to know something is wrong before users ever complain.

---

## 1. The Prometheus Data Model

Before you can query Prometheus, you need to understand how it organizes data. Every single data point Prometheus stores is essentially a timestamp and a number, tagged with a name and some labels.

**The Format:** `metric_name{label_name="label_value"} value timestamp`

- **`metric_name`** — What are we measuring? (e.g., `http_requests_total`)
- **`labels`** — Key-value pairs that add context. This is Prometheus's superpower. Instead of creating a new metric for every single endpoint, you use labels (e.g., `method="GET"`, `status="200"`, `pod="frontend-1"`).
- **`value`** — The actual number being measured (e.g., `1053`).
- **`timestamp`** — Exactly when this measurement was taken.

---

## 2. The 4 Metric Types

Prometheus tracks four types of numbers. Understanding the difference between these is crucial for writing correct queries.

1. **Counter** — A number that *only ever goes up* (or resets to zero if the app restarts).
   - *Example:* Total number of HTTP requests, total errors, distance driven in a car.
   - *Rule of thumb:* If you want to know "how fast" something is happening, you use a Counter.

2. **Gauge** — A number that can go up *and* down.
   - *Example:* Current CPU usage, memory consumption, active user sessions, the speedometer in a car.
   - *Rule of thumb:* If you're taking a current "snapshot" of a state, it's a Gauge.

3. **Histogram** — Samples observations and groups them into configurable "buckets."
   - *Example:* Request response times. You might have buckets for `<100ms`, `<500ms`, and `<1s`. This lets you calculate things like "95% of our requests finish in under 200ms" (the 95th percentile).

4. **Summary** — Similar to a Histogram (it tracks sizes and counts), but it calculates the percentiles directly on the client side (inside your app) before sending them to Prometheus. It's cheaper for Prometheus to process but less flexible to query than a Histogram.

---

## 3. How Prometheus Gets Data: Scrape Configs

Most monitoring tools use a "push" model — your application sends data to the database. **Prometheus uses a "pull" model.**

Your application just exposes a plain-text web page (usually at `http://your-app/metrics`) with its current vitals. Prometheus acts like a web scraper. Its **Scrape Configs** tell it:

1. *Where* to look (which IP addresses or Kubernetes services).
2. *How often* to look (e.g., every 15 seconds).

Prometheus goes to those addresses, reads the text file, and saves the numbers into its database.

---

## 4. PromQL: The Query Language

PromQL is how you ask Prometheus questions. Because it deals with time, it functions differently than SQL.

- **`rate()`** — Calculates the per-second average rate of increase of a **Counter** over a specific time window.
  - *Example:* `rate(http_requests_total[5m])` answers "On average, how many requests per second did we get over the last 5 minutes?"

- **`sum()`** — Adds numbers together. Usually combined with `by()`.
- **`by()`** — Groups the results by specific labels (like SQL's `GROUP BY`).
  - *Example:* `sum(rate(http_requests_total[5m])) by (status)` answers "What is the request rate, grouped by HTTP status code?"

- **`avg_over_time()`** — Takes a **Gauge** metric and averages it over a time window.
  - *Example:* `avg_over_time(memory_usage_bytes[1h])` answers "What was the average memory usage over the last hour?"

---

## 5. AlertManager & Recording Rules

**AlertManager:** Prometheus just stores data and evaluates rules. When a rule is broken (e.g., CPU > 80%), Prometheus fires an alert and sends it to AlertManager. AlertManager is a separate tool that acts as a dispatcher: it groups alerts, silences duplicates, and routes them to the right place (Slack, PagerDuty, Email, or the Aegis triage pipeline).

**Recording Rules:** Some PromQL queries are mathematically heavy (like calculating the 99th percentile of response times across 500 servers). If you put that query on a live Grafana dashboard, it will be incredibly slow. A **Recording Rule** tells Prometheus to run that heavy query in the background every few seconds and save the result as a *brand new, pre-calculated metric*.
