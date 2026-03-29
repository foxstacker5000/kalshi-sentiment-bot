# Kalshi Sentiment Bot

> Social sentiment moves Kalshi markets. By the time you read the thread, the price has already shifted. Kalshi Sentiment Bot monitors Twitter/X, Reddit, and Telegram in real time and enters positions before odds reprice.

*Last updated: March 2026*

![preview_kalshi sentiment bot](https://github.com/user-attachments/assets/d5e6f7a8-b9c0-4c1d-2e3f-4a5b6c7d8e9f)

## What is Kalshi Sentiment Bot?

Kalshi Sentiment Bot is a multi-source social sentiment engine for Kalshi. It monitors Twitter/X keywords, Reddit threads, and Telegram channels in real time, scores each sentiment signal on five dimensions, and alerts you - or automatically enters a position - when sentiment is shifting fast enough to precede a Kalshi market price movement.

Kalshi markets are driven by the same social narratives as any prediction market. Political sentiment on Twitter/X moves election contract prices. Economic discussion on Reddit moves rate and inflation markets. Sentiment Bot reads those shifts and acts before they reach the contract price.

---

## Download

| Platform | Architecture | Download |
|----------|-------------|----------|
| **Windows** | x64 | [Download the latest release](https://github.com/foxstacker5000/kalshi-sentiment-bot/releases) |

---

## Why Sentiment Moves Kalshi Markets

Kalshi contracts price real-world outcomes. Social platforms process information about those outcomes faster than any API. A breaking development on Twitter/X triggers hundreds of posts before a single Kalshi trader adjusts their contract price. The lag between social sentiment shift and Kalshi repricing is 5 to 14 minutes.

**Three sentiment windows Sentiment Bot catches:**

| Window Type | What Happens | Median Lead Time |
|------------|-------------|-----------------|
| **Breaking event** | News breaks on Twitter/X before Kalshi prices move | 5 to 11 min |
| **Narrative shift** | Reddit discussion flips tone on a slow-moving story | 9 to 22 min |
| **Momentum acceleration** | Volume of posts accelerates before prices move | 4 to 8 min |

---

## Five-Dimension Sentiment Scoring

| Dimension | What It Measures | Weight |
|-----------|-----------------|--------|
| **Source count** | Number of independent sources covering the event | 30% |
| **Velocity** | Rate of sentiment change over the last 15 minutes | 25% |
| **Source authority** | Follower count, subreddit size, channel subscribers | 20% |
| **Keyword match depth** | How precisely posts map to an active Kalshi market | 15% |
| **Momentum duration** | Whether the shift is sustained or a single spike | 10% |

A score of 70+ triggers an alert. A score of 85+ triggers optional automated entry. All thresholds configurable.

---

## Engine Features

* **Three live data streams** - Twitter/X keyword tracking, Reddit subreddit monitoring, Telegram channel reading, all processed simultaneously
* **NLP sentiment classifier** - transformer-based model tuned on prediction market event language
* **Kalshi market matcher** - maps each sentiment event to the closest active Kalshi market by topic and keywords
* **Velocity detector** - tracks sentiment delta over a configurable rolling window, not just absolute score
* **Multi-source confirmation** - requires signal to appear in at least N independent sources before scoring
* **Telegram alerts** - instant message with event summary, matched market, direction, score breakdown, and current contract price
* **Auto-entry mode** - enters position at your configured USD size when signal crosses the auto-entry threshold
* **Signal log** - every processed signal logged with match, score, direction, and any resulting trade

---

## Two Ways to Run It

| | Windows App | Python Bot |
|---|---|---|
| **Setup** | Double-click | `pip install` + config |
| **NLP model** | Bundled | Configurable |
| **Auto-entry** | Config-based | Custom sizing |
| **Config** | `config.toml` | Direct code access |
| **Alerts** | Dashboard + Telegram | JSON + Telegram |

## Quick Start

```
# 1. Download from Releases
# 2. Edit config.toml - add API keys, Kalshi credentials, and tracked keywords
# 3. Run Sentiment Bot - live scoring starts immediately
```

### Python

```bash
cd kalshi-sentiment-bot/python
pip install -r requirements.txt
python kalshi-sentiment-bot-v.1.0.2.py
```

---

## How It Works

![sentiment bot pipeline](https://github.com/user-attachments/assets/e6f7a8b9-c0d1-4e5f-3a4b-5c6d7e8f9a0b)

Five stages from social post to scored signal:

1. **Collect** - ingests posts from Twitter/X, Reddit, and Telegram matching your configured keywords
2. **Classify** - NLP model assigns sentiment score and extracts the core event claim
3. **Match** - maps the event to the closest active Kalshi market using topic keywords
4. **Score** - runs the five-dimension model on the matched signal
5. **Deliver** - signals below threshold are logged; signals above threshold trigger alert or auto-entry

### Config Reference

```toml
[sources]
twitter_keywords = ["kalshi", "fed rate decision", "election 2026", "bitcoin price"]
reddit_subreddits = ["politics", "worldnews", "economy", "CryptoCurrency"]
telegram_channels = []

[sentiment]
alert_threshold = 70
auto_entry_threshold = 85
auto_entry_usd = 30
velocity_window_minutes = 15
min_source_count = 3

[kalshi]
api_key = ""
api_env = "prod"

[filters]
min_market_volume_usd = 500
max_entry_price = 0.82
categories = ["politics", "economics", "crypto"]

[alerts]
telegram_bot_token = ""
telegram_chat_id = ""
```

---

## Verified on Kalshi

**Configuration used:**
* Sources: Twitter/X + Reddit (r/politics, r/economy), alert threshold 70, auto-entry at 85+

**High-score signal detected and auto-entered:**

| Event | Trade ID | Time |
|---|---|---|
| Auto-entry | trade_b8d0f2a4c6e8b0d2 | 2026-03-19 14:22:11 UTC |

**Signal breakdown:**
- Event: "Senate vote on budget resolution delayed, no deal before April"
- Source count: 7 independent sources
- Velocity: 0.54 delta in 15 min window
- Source authority: r/politics 8.2M members + verified Senate reporters
- **Total score: 87/100 - auto-entry triggered on NO at 0.39**

**Market resolved NO:**

| | Result |
|---|---|
| Settlement | 204 contracts x $1.00 |
| Cost | 204 contracts x $0.39 = $79.56 |
| Net P&L | +$124.44 on $79.56 deployed (156% ROI) |

---

## Frequently Asked Questions

**What is Kalshi Sentiment Bot?**
Kalshi Sentiment Bot monitors social platforms for sentiment shifts related to active Kalshi markets. It scores each signal on five dimensions and alerts or auto-enters when the score crosses your threshold.

**How is this different from a news bot?**
A news bot reads primary sources. Sentiment Bot reads the social reaction - which includes volume, velocity, and cross-platform spread. The two approaches are complementary and can run simultaneously.

**Does it need a Kalshi API key?**
Only if auto-entry is enabled. In alert-only mode, the bot reads social data and sends Telegram alerts without accessing Kalshi.

**Is Kalshi available outside the US?**
Kalshi is a US-regulated exchange. Check Kalshi's current geographic restrictions before use.

**Does it work on Linux?**
Yes. The Python version runs on any platform with Python 3.10+. The Windows .exe is Windows-only.

---

## Use Cases

- **Political market sentiment trading** - detect Twitter/X narrative shifts on election and legislation markets before Kalshi reprices
- **Economic market entry** - monitor r/economy and financial Twitter for early reads on Fed rate and CPI markets
- **Pre-reprice entry** - enter 5 to 14 minutes before social sentiment shifts Kalshi contract prices
- **Multi-source confirmation** - require sentiment agreement across Twitter/X + Reddit before entering any position
- **Crypto price market trading** - monitor crypto Twitter for early signals on BTC/ETH price markets on Kalshi

---

## Repository Structure

```
kalshi-sentiment-bot/
+-- kalshi-sentiment-bot-v.1.0.2.exe
+-- config.toml
+-- data/
|   +-- signals/
|   +-- sentiment_cache/
|   +-- logs/
+-- python/
|   +-- src/
|   |   +-- collector.py
|   |   +-- nlp_scorer.py
|   |   +-- market_matcher.py
|   |   +-- alerts.py
|   |   +-- executor.py
|   +-- scripts/
|   |   +-- backtest_sentiment.py
|   +-- requirements.txt
+-- README.md
```

---

## Requirements

```
python-dotenv, typer[all], httpx, praw, tweepy, transformers, torch, devtools
```

* Twitter/X API v2 credentials (Basic tier)
* Reddit API credentials via PRAW (free)
* Kalshi API key (only if auto-entry enabled)

---

*Read the room. Trade Kalshi first.*
