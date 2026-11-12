# IV contact verification (email, SMS or WhatsApp)

Prototype of a new last step in the Chekin guest app identity verification (IV): after the document and selfie photos, the guest adds an email **or** a mobile number (one channel, set by the host) and confirms it with a 6-digit code. Built on top of a static replica of the guest app v2.

**Open it:** [mobile + desktop](https://dclemares.github.io/iv-contact-verification/split.html?s=g2-iv) · [mobile](https://dclemares.github.io/iv-contact-verification/screens/g2-iv.m.html) · [desktop](https://dclemares.github.io/iv-contact-verification/screens/g2-iv.d.html)

## Flow
Document → photos → **contact step (2 screens)** → Verifying your identity → Identity verified (shows the confirmed contact). The guest's email or phone is not known beforehand, so the field starts empty.

1. **Add your email / mobile / WhatsApp number**
   - Two-segment progress at the top: «Add number · Enter code».
   - Subtitle: a 6-digit code will be sent (by email / by SMS / on WhatsApp) and entered on the next screen.
   - One white card: country on its own row (defaults to the scanned document's country) and a large number field — or a single email field.
   - Email typo help (gmial.com → gmail.com, tap to fix); explains an incomplete email or a too-short number.
   - CTA names the channel: «Send code», «Send code by SMS», «Send code on WhatsApp».
2. **Enter the code**
   - One white card: «Sent by SMS to +34 616 537 158» with Edit, then the 6 boxed digits with the expiry pill. The code is checked automatically on the 6th digit (no verify button).
   - Under the digits: **Paste code** (fills a code copied from WhatsApp's «Copy code») and **Didn't get the code?**, which opens a bottom sheet with a channel tip and: resend (after 0:30), get it on the other channel — SMS ⇄ WhatsApp, same number — (after 0:30), call me with the code (after 1:00). For email: resend or use a different email.
   - 3 tries per code («N tries left»), then «Too many tries» until a new code is sent. Expiry: 10 min (email), 5 min (SMS, WhatsApp).
   - On desktop the code sits in a centred 440 px column.

## Controls (Controls panel)
- **Contact verification** (booking settings): Off · Email · SMS · WhatsApp.
- **Contact step › Go to contact step**: jumps straight to the step (on mobile + desktop, both screens jump).
- **Contact code (next try)**: Correct · Wrong.

Demo codes: email `482791`, SMS and WhatsApp `913604`. A simulated notification (Mail, Messages or WhatsApp) drops in after sending; tapping it fills the code.
