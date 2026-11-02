# Five loops you can copy tonight

Loop engineering means you stop prompting an agent step by step and set up a loop that keeps it working until the job is actually done. The Claude Code team describes the kinds of loop in [Getting started with loops](https://claude.com/blog/getting-started-with-loops). Two of them are the ones you set up yourself:

| | Goal loop (`/goal`) | Time loop (`/loop`, `/schedule`) |
|---|---|---|
| Starts | You give it a goal | A clock: every 5 minutes, every morning |
| How it works | It works, tries to stop, and a separate checker asks "is it done?". If not, it goes back to work | It runs the same job again and again, looks at what changed and acts on it |
| Stops | The goal is met, or it hits the number of tries you allowed | You turn it off |
| Use it for | Work where "done" can be checked: a score, a count, a rule | Recurring work, and watching things outside your computer |

`/loop` runs on your own computer and stops when it sleeps; `/schedule` runs in the cloud. Check the [Claude Code docs](https://code.claude.com/docs) for what's available on your plan: some of these are research previews.

The rule that makes any loop work: **"done" has to be something the agent can check by looking at the real result**, not something it can just claim. Each loop below says what it checks and when it stops. Pair them with the review loop in this repo when you want an independent reviewer to judge the result.

---

## 1. Goal: a fast homepage on a phone

```
/goal My homepage scores 90 or above for Performance in Lighthouse, mobile settings.
Run Lighthouse after every change and use that score, not your own estimate.
Don't change how the page looks or what it says. Stop after 5 tries and tell me what's left.
```

**Checks:** a real Lighthouse run (`npx lighthouse <url> --preset=perf --form-factor=mobile`, or Chrome DevTools).
**Stops:** score ≥ 90, or 5 tries.
**Usually finds:** huge images, fonts loaded the slow way, scripts that block the page.

## 2. Goal: every word readable without JavaScript

Many AI crawlers read the HTML your server sends and don't run your JavaScript. If an animation starts your text invisible and fades it in, they may never see it.

```
/goal Every piece of text a visitor can read on my pages is also in the page's HTML
and readable with JavaScript turned off.
To check: fetch each page's raw HTML (curl, no browser) and compare it with what the
browser shows; also load it with JavaScript disabled. Keep the animations, but make the
text visible by default and let the animation add the effect.
Stop when every page passes, or after 5 tries per page, and list what you changed.
```

**Checks:** the raw HTML and a no-JavaScript load, against the visible page.
**Stops:** no missing text on any page.
**Usually finds:** fade-in text that starts at `opacity: 0`, counters that start at 0, tab content that only exists after a click, a whole page rendered only in the browser.

## 3. Goal: a video with nothing in the cropped area

Phones crop a 9:16 video differently, and Instagram covers parts of a reel with its own buttons and captions.

```
/goal Render the video, then check frames every second: no text or key visual sits in the
area the phone crops off or the app covers.
Safe area for a 1080x1920 reel: keep text between x 150 and 940 and between y 250 and 1500.
Extract the frames, shade the unsafe areas, and look. Fix and render again until no frame fails.
Stop after 5 renders and show me the frames that still fail.
```

**Checks:** real frames from the rendered file, not the code.
**Stops:** every checked frame is clean.
**Usually finds:** captions that run under the app's buttons, text touching the edge on tall phones.

## 4. Time: your contact form, every morning

A form that quietly stops sending loses enquiries, and nobody notices until a customer asks why you never replied.

```
/schedule every day at 08:00: send a test enquiry through the contact form on <my site>
with the subject "Daily form test <date>". Then check <my inbox / CRM> for it.
If it hasn't arrived within 10 minutes, message me straight away with what you saw.
If it has, delete the test enquiry and stay quiet.
```

**Checks:** the enquiry actually arriving, not the form saying "thank you".
**Runs:** every morning until you turn it off.
**Usually finds:** an expired email password, a spam filter, a form plugin that updated and broke.

## 5. Time: your ad numbers, every morning

Meta's count of purchases and your shop's real orders drift apart when tracking breaks, and the money keeps going to the wrong ads until someone notices.

```
/schedule every day at 09:00: get yesterday's purchases from Meta Ads Manager and
yesterday's paid orders from <my shop>. Compare them.
If Meta's number is more than 20% below the shop's, or above it at all, tell me, with
both numbers and the date it started. Otherwise stay quiet.
```

**Checks:** two real numbers from two real systems.
**Runs:** every morning until you turn it off.
**Usually finds:** a pixel removed in a site update, sales counted twice, a tracking setup that stopped sending.

The 20% is a starting point: some gap is normal, because Meta only counts sales it can link to an ad. Learn what your usual gap is in the first week, then tighten it.

---

Made by Aliz ([@builtbyalizz](https://instagram.com/builtbyalizz)). Found a loop that works? Open an issue and share it.
