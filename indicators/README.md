# Indicators

TradingView Pine Script studies kept alongside this repo.

## ws-killzones.pine

Session / killzone highlighter. Draws a high-low box around the **Paris**,
**London**, **New York** and **Asia** sessions and can background-highlight up to
four extra time windows.

**Install:** TradingView → Pine Editor → paste the file contents → *Add to chart*.

### Settings

| Group | Input | Notes |
|---|---|---|
| Sessions | Maximum box count | Past boxes kept per session (applies on every timeframe) |
| Sessions | Line width | Box border width |
| Sessions | Show session labels | Optional name label at each session start |
| Sessions | Use custom time zone | Off = exchange time; on = the IANA zone you type (e.g. `America/New_York`) |
| Sessions | Paris / London / New York / Asia | Enable, session time, border colour, background colour |
| Additional Sessions | Trading Session 1-4 | `bgcolor` highlight with its own colour and transparency |

### Notes

* The Paris, London and Asia background colours default to fully opaque, so the
  boxes cover the candles. Lower the opacity in the colour picker if you want the
  price action visible through them.
* Border colours default to `…00` alpha (fully transparent borders).
