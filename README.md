# seeknull.github.io

Served at <https://seeknull.github.io/>. Add whatever you like — with two exceptions.

## Do not move these

```
.well-known/assetlinks.json   OTP Relay depends on this, at exactly this path
r/index.html                  landing page for OTP Relay request links
```

**`.well-known/assetlinks.json` must stay at the domain root.** Android verifies app links with
Digital Asset Links, which is looked up per host and only ever at `/.well-known/assetlinks.json`.
It cannot live inside `/r/` or anywhere else. If it moves or breaks, request links stop opening the
OTP Relay app and fall back to the browser.

It lists two certificate fingerprints, the release key and the debug key, so both builds work.

**`/r/` belongs to OTP Relay.** Shared request links look like:

```
https://seeknull.github.io/r/#to=%2B919...&mins=15
```

The details sit after the `#`, which browsers never send to the server, so the phone number never
reaches GitHub's logs. `r/index.html` is only what a visitor sees when the app is not installed.
Links already sent to people keep working as long as this path exists.

## Everything else is free

The app declares `pathPrefix="/r/"`, so it only ever intercepts URLs under `/r/`. Every other page
on this domain opens in the browser as normal, and `index.html` is not used by the app at all.

`.nojekyll` is there so GitHub Pages serves the `.well-known` directory; Jekyll skips dot-folders.
