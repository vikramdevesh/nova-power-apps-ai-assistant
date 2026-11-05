# Nova – a ChatGPT-style AI assistant built in Power Apps

Two "crazy UI" phone apps from the **LowCodeStudio** YouTube video *I built a ChatGPT-style AI app in Power Apps*:

| App | Data | Controls |
|---|---|---|
| **Nova Weather** | MSN Weather connector (free, no API key) | 16 |
| **Nova Sales** | SharePoint list `Nova Deals` (live, auto-refresh) | 21 |

Both have an animated SVG "AI orb" that changes colour with Nova's state, answers that type themselves out,
quick-question chips and a free-text ask bar.

```
nova-weather-phone.yaml paste-ready controls for Nova Weather
nova-sales-phone.yaml   paste-ready controls for Nova Sales
nova-deals.csv          the 40 sample deals behind Nova Sales
```

## Nova Weather
1. Create a **blank canvas app, Phone layout**.
2. **Data → Add data → MSN Weather**.
3. Select the screen and set **Fill** to `RGBA(5, 6, 15, 1)`.
4. Open `nova-weather-phone.yaml`, copy everything, then right-click the screen → **Paste**.
5. Press **Play**. Change the city in the box at the top and tap a chip, or type your own question.

## Nova Sales
1. **Create the SharePoint list** `Nova Deals` (Site contents → New → List → *From CSV*, pick
   `nova-deals.csv`). Set the column types:

   | Column | Type |
   |---|---|
   | Title | Single line of text |
   | Amount | Currency |
   | Stage | Choice: Prospecting, Qualification, Proposal, Negotiation, Closed Won, Closed Lost |
   | Region | Choice: North, South, East, West |
   | Owner | Single line of text |
   | Probability | Number |
   | CloseDate, LastActivity | Date |

2. Create a **blank canvas app, Phone layout**, then **Data → Add data → SharePoint** → your site → `Nova Deals`.
3. Set the screen **Fill** to `RGBA(5, 6, 15, 1)`.
4. Copy all of `nova-sales-phone.yaml` and paste it onto the screen.
5. Press **Play**. The KPIs count up and Nova greets you with live numbers.
   Change a deal's **Stage** to *Closed Won* in SharePoint and watch the app celebrate within a few seconds.

> The sample dates are around November 2026, because "this quarter" is worked out from `Today()`.
> If you build this later, shift `CloseDate` / `LastActivity` in the CSV so some deals fall in the current quarter.

## How the orb works
It's a single **Image** control whose `Image` property is an SVG built with a formula:
a radial gradient (3D sphere), a blurred copy behind it (glow), two blurred blobs spinning in opposite directions
clipped to the circle (liquid swirl), a soft highlight (glass) and a CSS "breathe" animation.
One variable – `varOrbState` (idle / listening / thinking / speaking) – drives the colours and speed.

---
Made by **Devesh Vikram Singh** for LowCodeStudio on YouTube.
Free to use and adapt.
