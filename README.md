# गिरवी बही — Girvi Bahi (phone app)

An offline girvi register, old gold/silver purchase book, and GST billing for new jewellery — for one shop. Everything lives on the shopkeeper's phone, locked with a PIN. Nothing is sent to any server.

## Files
- `index.html` — the whole app
- `sw.js` — makes it work without internet after the first open
- `manifest.webmanifest`, `icon-192.png`, `icon-512.png` — let Android install it like an app

## Put it on the phone (one time, ~10 minutes)
The phone has to load the app once from an `https://` link. After that it runs offline from the phone. The link only serves these files; no data goes there.

1. Create a GitHub repo (it can be private if you have GitHub Pro, otherwise public — the code has no data in it).
2. Upload these 5 files to the repo root.
3. Repo → Settings → Pages → Deploy from branch → `main` / root. Wait a minute for the `https://<you>.github.io/<repo>/` link.
4. On his phone, open the link in **Chrome** → menu ⋮ → **Add to Home screen / Install app**.
5. Open it from the home screen → set the PIN → write down both recovery codes:
   - **Shop code** → in his register
   - **Helper code** → with you
6. Settings → enter today's gold and silver rates, the shop name, his buying margins, and under "GST & bills": registration type, GSTIN, address, making %, old-gold deduction %, and the highest discount allowed. Confirm the GST settings and bill format with his CA before the first real bill.

Updating later: change the files, bump `VERSION` in `sw.js`, push. The phone picks it up the next time it opens online.

## How the data is kept safe
- The register and every photo are stored scrambled on the phone. The PIN (or either recovery code) unlocks the key; without one, the data is unreadable.
- Locks itself after the chosen time, or with the 🔒 button. 5 wrong PINs → it waits before allowing more tries.
- **Backup** (home screen reminds after 7 days): shares one file to Google Drive, Gmail or WhatsApp. The file is scrambled the same way — it opens only with the PIN or a recovery code of that phone.
- **New / lost phone:** install the app → "Bring back a backup" → choose the file → old PIN or a recovery code.

## Not done yet (on purpose)
- Automatic backup or sync to Google Drive / Gmail — today it's one tap, by hand.
- Live gold/silver rates — set `RATES_URL` in `index.html` to an endpoint that returns `{"gold24_10g":..., "silver_kg":..., "date":"YYYY-MM-DD"}` and the app fetches it on open.
- Tested in desktop Chrome with a phone-sized screen, offline mode, backup and restore. Not yet tested on a real Android phone — do a full dry run with dummy entries before he relies on it.
