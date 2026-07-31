# Saifu 財布

A tiny offline bill splitter for eating out with friends — including the awkward couple case, where two people pay from one wallet.

No accounts, no server, no AI. One HTML file; all the maths runs in the browser and your crew is saved in the device's local storage.

## What it does

- **Split a bill evenly** between everyone who was actually there (tap ✓ to include or sit someone out).
- **Couples pay as one wallet** — tap ♡ on two people to pair them. They still count as two shares, but the result is a single amount owed to the payer.
- **"Just for one" items** — a dish or drink only one person had comes out of the shared pot and goes onto their tab.
- **Whoever paid** can change per outing; the summary always reads *who pays who*.
- **Rounding** to a clean number (¥10 / ¥100 and equivalents); the payer absorbs the difference so the total always balances.
- **Currencies** — JPY by default, plus USD, EUR, GBP, KRW, TWD, THB, SGD, AUD, VND.
- **Copy the summary** as plain text to paste into a group chat.

## How the maths works

```
shared        = total − sum(just-for-one items)
per head      = shared ÷ number of people eating
someone's share = per head + their own items
a wallet owes = sum of its members' shares   (rounded)
payer gets back = total − everything collected
```

## Use it

Open `index.html` in any browser — that's it, it works offline.

**Install on a phone (home-screen app):** serve the repo over https (GitHub Pages, Netlify), open it in the phone's browser and choose *Add to Home Screen* / *Install app*. iOS cannot install a page opened from a local file, so it has to be served.

For an installable build, keep these next to `index.html`: `manifest.webmanifest`, `sw.js`, `icon-180.png`, `icon-512.png`.

## Look & feel

Warm cream ground, terracotta and sage accents, over-rounded shapes, Fredoka over Nunito, and a hand-drawn dog-doodle background.

## Privacy

Nothing leaves the device. The only stored data is your saved crew, currency and rounding preference, in `localStorage` under `warikan.crew.v1`.
