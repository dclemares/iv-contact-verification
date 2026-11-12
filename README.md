# IV contact verification (email or SMS)

Prototype of a new last step in the Chekin guest app identity verification (IV): after the document and selfie photos, the guest adds an email **or** a phone number (one channel, set by the host) and confirms it with a 6-digit code. Built on top of a static replica of the guest app v2.

**Open it:** https://dclemares.github.io/iv-contact-verification/screens/g2-iv.m.html (mobile) · [desktop](https://dclemares.github.io/iv-contact-verification/screens/g2-iv.d.html) · [mobile + desktop](https://dclemares.github.io/iv-contact-verification/)

## Flow
Document → photos → **Add your email / phone number → code** → Verifying your identity → Identity verified (shows the confirmed contact). The guest's email or phone is not known beforehand, so every version starts with an empty field.

## Controls (bottom-left «Controls» panel)
- **Contact verification**: Off · Email · SMS.
- **Contact step version (jumps to it)**: jumps straight to the step.
  - **Current**: add your email/phone screen, then a code screen.
  - **1 · Direct**: one screen; after sending, the field becomes a «Sent to … Edit» row and the code card appears below.
  - **2 · Sheet**: one card with the field; the code is typed in a bottom sheet (a centered dialog on desktop).
  - **3 · Keypad**: dark «Code sent to» card, large digits and an on-screen numeric keypad on mobile.
  - **4 · Link**: we send a link (plus a code); tapping it continues automatically, with «Enter the code instead» as a fallback.
- **Contact code (next try)**: Correct · Wrong.

Demo codes: email `482791`, SMS `913604`. A simulated system notification with the code drops in after sending; tapping it fills the code (in version 4 it acts as the link).

Common details: 6-digit one-time-code input, 2-minute expiry countdown, resend after 30 s, expired-code state, wrong-code state, auto-check on the 6th digit.
