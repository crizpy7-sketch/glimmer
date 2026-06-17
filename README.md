# Glimmer — Reveal Studio

Glimmer is a one-file web app that lets anyone create a beautiful **tap-to-reveal**
announcement — gender reveal, pregnancy, engagement, new home, graduation,
holiday card and more — and share it as a link. No app, no account.

You run it as a tiny business: people make reveals for free, and you sell them a
**$3 Premium bundle** (printable card + "guess" link + extra captions) through
**your own Stripe**. The money goes straight to you.

There's no backend and no build step — it's a single `index.html` you can host
anywhere.

---

## How the money works (read this first)

1. **You** deploy the page and connect **your** Stripe Payment Link.
2. **Visitors** open your link and build a reveal for free.
3. When they want the extras, they tap **"Unlock everything · $3"**, which opens
   **your** Stripe checkout. The $3 lands in **your** account.

So "the premium stuff" is what *buyers* pay you for — not something you unlock for
yourself. To see exactly what you're selling, use **gear → Connect Stripe →
"👀 Preview what buyers unlock"** (no payment needed).

---

## Launch checklist

### 1. Create your Stripe Payment Link (≈3 min)
- Make a free [Stripe](https://stripe.com) account.
- Dashboard → **Payment Links** → **+ New** → set the price to **$3** (or whatever
  you choose) → **Create link**.
- Copy the URL — it looks like `https://buy.stripe.com/xxxxxxxx`.
- *(Optional but recommended)* In the Payment Link settings, set the **success URL**
  to `https://YOURSITE/?unlocked=1` so buyers are auto-unlocked when they return.

### 2. Deploy the page (≈2 min)
Any static host works. Easiest options:
- **Netlify Drop** — drag the folder onto <https://app.netlify.com/drop>.
- **GitHub Pages** — repo → Settings → Pages → deploy from `main`.
- **Cloudflare Pages / Vercel** — point at this repo.

Make sure `index.html` and `og.png` are deployed together.

### 3. Connect Stripe (≈1 min)
- Open your live site and add `?setup=1` to the URL the first time:
  `https://YOURSITE/?setup=1`
- Tap the **gear** (top-right) → **Connect Stripe**:
  - **Brand name** — what your reveal studio is called.
  - **Stripe Payment Link** — paste the URL from step 1.
  - **Price label** — e.g. `$3`.
- Tap **Apply & preview**, then **Copy my live link**.

> **The gear is owner-only.** It shows for you (unconfigured site, `?setup=1`, or
> once you've set up on this device). The live link you share has no `?setup`, so
> **visitors and buyers never see the gear.** Lost access on a new device? Just
> open `https://YOURSITE/?setup=1` again.

### 4. Share & promote
- The **live link** from step 3 is the URL you put in your bio, posts, and ads.
- The gear → **Promote it** tab has ready-to-post hooks, a story, an ad caption,
  and a one-tap **demo link** to show the experience off.
- For pretty link previews, keep a `1200×630` **`og.png`** next to `index.html`.

---

## Good to know

- **No accounts, nothing stored on a server.** Each reveal lives entirely inside
  its own link (the part after `#`). Your Stripe/brand setup is remembered in your
  browser and carried in your live link's query string.
- **Unlocking is an honor system.** After checkout the buyer taps "I've completed
  my payment → unlock." There's no server verifying the payment, so a dishonest
  person *could* unlock without paying. That's the trade-off for being backend-free
  — fine for a $3 impulse buy. Hardening it would require a small serverless
  function.
- **Occasions & moods.** The big reveal colour comes from the **occasion**
  (pink/blue, gold, etc.). A **mood** sets the lead-up scene the guest sees before
  tapping and tints the confetti.
- **Customise copy.** The announcement and caption text is generated in
  `index.html` from template pools — search for `OCCASIONS` to edit wording, add
  occasions, or change palettes.
- **⚠️ Replace placeholder social proof.** The testimonials and the
  "14,000+ families · 4.9" stat near the top are **illustrative placeholders**
  (marked `[EDIT]` in `index.html`). Swap in your own real numbers/reviews before
  running ads — shipping invented stats as fact is misleading.

---

## File layout

```
index.html   ← the entire app (markup, styles, logic)
og.png       ← social share preview image (1200×630)
README.md    ← this guide
```

That's it. Open `index.html` locally to try it, or deploy it to go live.
