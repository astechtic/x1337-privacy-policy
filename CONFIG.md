# App config

- `config_v2.json`: read by the new app (redesign build). Every value is real JSON: objects, arrays, numbers, booleans.
- `config.json`: read by older app versions, where values are JSON inside strings. Keep it until old versions are gone. The new app falls back to it if `config_v2.json` can't be loaded.

## config_v2.json

```json
{ "version": 2, "ADS_DATA": [], "CONFIG": { "KEY": value } }
```

| Key | Type | What it does |
|---|---|---|
| `ENABLE_PRO` | bool | Paywall, Pro and RevenueCat. Off: Pro features are free for everyone. |
| `ENABLE_ADS` | bool | House banners, ad SDKs, unlock sheet. Off: no ads. |
| `SUPPORTING_BUSINESS_AD` | object | 5th tab: `image`, `label`, `enable`, `onImageTapAction` (`openUrl` opens outside the app), `onImageTapUrl`. |
| `BOOK_SEARCH_SITES_DATA` | array | Websites searched. Optional `categories`: file type (`video`, `audio`, `app`, `game`, `book`, `archive`) → search path used when that type is picked in "Search in". |
| `TRENDING_QUERIES` | array of strings | Home › Trending today. |
| `TRENDING_UPDATED_AT` | ISO date or unix time | "Updated N h ago" on Trending. Update it when you change the list. |
| `WELCOME_EXAMPLES` | array of `{label, query, type}` | Example searches on the Welcome screen. |
| `HOME_CATEGORIES` | array of `{label, query, type}` | Home categories (`type` like `ISO`, `MKV`, `MP3`, `APP` also sets the file-type filter). |
| `FREE_ALERT_LIMIT` | int | Free saved-search alerts (default 3). |
| `FREE_LINK_OPENS_PER_DAY` | int | Link opens before the unlock sheet when ads are on (default 5, 0 = off). |
| `MIN_FULLSCREEN_AD_INTERVAL_SEC` | int | Minimum seconds between full-screen ads (default 120). |
| `PAYWALL_VARIANT` | string | `default`, `no_trial` or `monthly_first`. |
| `ENABLE_INTERSTITIAL_ADS`, `ENABLE_ADS_ON_*` | bool | Old ad switches, kept off. |

Not set yet (the app has fallbacks):

- `TERMS_URL`: terms of use page for the paywall. Falls back to the privacy policy.
- `SUPPORT_EMAIL`: "Send feedback" opens an email with app details. Falls back to the Google Form.
- `APP_OPEN_ROUTE`: a deep link opened once on app start.
- `ENABLE_IRON_SOURCE`, `IRON_SOURCE_REWARDED_AD`, `IRON_SOURCE_INTERSTITIAL_AD`: LevelPlay ad units.
- `AD_PLACEMENTS`: object of slot → bool to switch single house-ad slots off.
