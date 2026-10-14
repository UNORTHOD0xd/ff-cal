# ff-cal

A USD economic calendar (Forex Factory, high + medium impact) published as an
iCal feed you can subscribe to on iPhone, Google Calendar or Outlook.

A GitHub Actions workflow fetches Forex Factory's weekly feed every 3 hours,
keeps only USD high and medium-impact events, and commits `docs/usd.ics`.
GitHub Pages serves it.

- 🔴 high impact (with a 10-minute alert) · 🟠 medium impact
- Event notes show the forecast and previous values
- If Forex Factory is unreachable, the build fails and the last good calendar stays live

## Setup

1. Create a **public** repo named `ff-cal` and add these files, keeping the folder structure.
2. **Settings → Actions → General → Workflow permissions**: choose **Read and write permissions** and save.
3. **Actions** tab → **Build calendar** → **Run workflow**. It should finish green and commit `docs/usd.ics`.
4. **Settings → Pages**: Source **Deploy from a branch**, branch **main**, folder **/docs**, then save.
5. After a minute, open `https://<username>.github.io/ff-cal/` and tap **Subscribe on iPhone**.

Feed URL: `https://<username>.github.io/ff-cal/usd.ics`

## Notes

- Forex Factory's public feed only covers the current week.
- The 3-hour schedule is in `.github/workflows/build-calendar.yml`; GitHub may run scheduled jobs a few minutes late.
- To change the filter, edit `CURRENCIES` and `IMPACTS` at the top of `scripts/build-ics.mjs`.
- Test locally: `node scripts/build-ics.mjs docs/usd.ics` (Node 18+).
