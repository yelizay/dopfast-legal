# Drafts — workflow notes

Files in this directory are **awaiting legal review**. They are not the live
policies — those are at the repo root and served at:

- `https://legal.dopfast.com/privacy-policy.html`
- `https://legal.dopfast.com/terms-of-use.html`

The drafts here are served at the `/drafts/` path and are visible to reviewers
but **not** linked from the iOS app or the marketing site. That's deliberate —
it lets lawyers + co-founders poke at revised copy without affecting what
real users see.

## How the swap works

1. Drafts written here and deployed (`npx wrangler deploy` from the repo root
   redeploys everything including `/drafts/*`).
2. Lawyer reviews at `legal.dopfast.com/drafts/privacy-policy.html` /
   `terms-of-use.html`, suggests changes.
3. Iterate on the draft files in this folder until sign-off.
4. On sign-off: move the draft files up one level, replacing the live ones:

   ```bash
   cd /Users/buraksoci/Projects/Personal/dopfast-legal
   mv drafts/privacy-policy.html privacy-policy.html
   mv drafts/terms-of-use.html terms-of-use.html
   npx wrangler deploy
   ```

5. Update the four iOS link references:
   - `Dopfast/Views/Settings/SubscriptionView.swift:174, 182`
   - `Dopfast/Views/Settings/SettingsView.swift:378, 393`

   to point at `https://legal.dopfast.com/privacy-policy.html` /
   `terms-of-use.html` (currently they still point at the old GitHub Pages
   URLs at `yelizay.github.io/dopfast-legal/*`).

6. Commit + push from both `origin` (yelizay) and `solenos` remotes, since the
   live policies are considered the company's entity-level legal record.

## Why we stage like this

- **No user-facing breakage during review.** The live privacy + terms stay
  stable while the drafts change.
- **Reviewers get a real URL to read**, not a PDF attachment or copy-pasted
  text.
- **Version history is preserved.** After the swap, the superseded live
  versions are still recoverable from git history.

## Revisions in the current drafts (vs live 2026-04-15 versions)

See the HTML comment block at the top of each draft file for the full changelog.
Key shifts:

- Minimum age raised from 9+ to **18+** (Anthropic Commercial Terms §2).
- Cloudflare Inc., RevenueCat Inc. added as disclosed subprocessors.
- Anthropic's 30-day API retention window stated explicitly.
- Anonymous per-install device identifier disclosed and GDPR-treated.
- GDPR, CCPA, and international-transfer sections added to privacy policy.
- Terms-of-Use: §7 (Acceptable Use) flows Anthropic's AUP to end users;
  new §8 forbids safety-system circumvention; new §10 lists crisis resources
  prominently; new §15 permits termination for AUP violations.
- Contact email moved from `support@dopfast.ai` to `support@solenos.com`.
