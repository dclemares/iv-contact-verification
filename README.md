# IV contact verification (email, SMS or WhatsApp)

Prototype of a new last step in the Chekin guest app identity verification (IV): after the document and selfie photos, the guest adds an email **or** a mobile number (one channel, set by the host) and confirms it with a 6-digit code. Built on top of a static replica of the guest app v2.

**Open it:** https://dclemares.github.io/iv-contact-verification/screens/g2-iv.m.html (mobile) · [desktop](https://dclemares.github.io/iv-contact-verification/screens/g2-iv.d.html) · [mobile + desktop](https://dclemares.github.io/iv-contact-verification/split.html?s=g2-iv)

## Flow
Document → photos → **Add your email / mobile / WhatsApp number → code** → Verifying your identity → Identity verified (shows the confirmed contact). The guest's email or phone is not known beforehand, so every version starts with an empty field.

## Controls (bottom-left «Controls» panel)
- **Contact verification** (booking settings): Off · Email · SMS · WhatsApp.
- **Contact step version (jumps to it)**:
  - **Current**: add your email/number screen, then a code screen.
  - **1 · Direct**: one screen; after sending, the field becomes a «Sent to … Edit» row and the code card appears below.
  - **2 · Sheet**: one card with the field; the code is typed in a bottom sheet (a centered dialog on desktop).
  - **3 · Keypad**: dark «Code sent to» card, large digits and an on-screen numeric keypad on mobile.
  - **4 · Link**: we send a link (plus a code); tapping it continues automatically, with «Enter the code instead» as a fallback.
  - **5 · Native**: modelled on WhatsApp's own number verification and Twilio Verify / Uber fallbacks. Country on its own row (defaults to the document's country) and a large number field, CTA «Send code» → «Verify your number» with the code in a white card (header, expiry, single-line «––– –––» digits that check themselves, no verify button) and «Wrong number?» → «Didn't get the code?» list: Resend SMS / on WhatsApp (0:30), get it on the other channel (0:30), Call me with the code (1:00); for email: Resend email, Open mail app, Use a different email.
  - **6 · Focus** (on top of 5): a two-segment progress «Add number · Enter code»; everything in one white card (icon + «Your mobile number», country, number); CTA names the channel («Send code on WhatsApp»). Code screen: destination row with Edit inside the same card, boxed digits, expiry, a «Paste code» chip (for codes copied from WhatsApp's «Copy code»), and, next to it, «Didn't get the code?», which opens the same help sheet as version 7.
  - **7 · Smart** (on top of 5): for phone channels the guest picks where the code arrives — WhatsApp («Usually the fastest») or SMS («Works on any phone») tiles; for email, one-tap domain chips (@gmail.com, @hotmail.com…). Code screen: one white card with a countdown ring around the channel icon, destination with Change, digits; fallbacks hidden behind «Didn't get the code?», which opens a bottom sheet with a channel-specific tip.
  - **8 · Preview** (on top of 5): under the field, «What you'll receive» shows a mock of the real message (WhatsApp chat with verified sender and «Copy code», SMS bubble or inbox row) so the guest recognises it. Code screen: the same message with «Delivered ✓✓» / «Sent just now», then «Type the code here» white card and the fallback list.
- **Contact code (next try)**: Correct · Wrong.

Demo codes: email `482791`, SMS and WhatsApp `913604`. A simulated notification (Mail, Messages or WhatsApp) drops in after sending; tapping it fills the code (in version 4 it acts as the link).

## Common to every version
- **What happens next**: «Last step» eyebrow and a neutral subtitle (no «we») saying a 6-digit code will be sent to the email or number and that the guest enters it next.
- **Phone field**: the country code defaults to the country of the scanned document; 24 common codes with flags.
- **Field checks**: suggests the right domain for common email typos (gmial.com → gmail.com, tap to fix); explains an incomplete email or a too-short number after leaving the field.
- **SMS ⇄ WhatsApp**: with a phone channel, once resend is available (and on expired or locked codes) the guest can get the code on the other channel for the same number. Version 4 offers it while waiting for the link.
- **Code**: 6-digit one-time-code input, auto-check on the 6th digit, resend after 30 s, expiry 10 min (email) / 5 min (SMS, WhatsApp), 3 tries per code with «N tries left», then «Too many tries» until a new code is sent.
- **Open the app**: «Open mail app» for email, «Open WhatsApp» for WhatsApp.
