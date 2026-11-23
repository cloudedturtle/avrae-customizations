# !weather

Part of the **Triboar Book Club Collection**.

Rolls and tracks the current weather for the Dessarin Valley, persisting
the result between calls via a uvar (`dessarin_weather`).

## Usage

- `!weather` — advance one day. Rolls 1d6 for persistence: on a 1-3 the
  current weather holds, on a 4-6 a fresh 1d8 is rolled.
- `!weather new` / `!weather reroll` — force a fresh 1d8 roll, ignoring
  persistence.
- `!weather show` — redisplay the current weather without rolling.
- `!weather set <1-8>` — DM override: set the weather to a specific
  result (1-8, see table below) without rolling.

## Results (1d8)

| Roll | Weather | Mechanical effect |
| --- | --- | --- |
| 1 | Clear skies | None. |
| 2 | Low river mist | Visibility 60 ft until midmorning. |
| 3 | Steady drizzle | Disadvantage on tracking checks. |
| 4 | Hard wind | Disadvantage on ranged attacks beyond normal range. |
| 5 | Passing showers | None. |
| 6 | Cold, soaking rain | Half travel speed through open country. |
| 7 | Thunderstorm | Visibility 30 ft. |
| 8 | Unnatural stillness | None. Something large may be nearby. |

Outputs an embed with the current weather, flavor text, mechanical
effect, and (when rolled) the dice results. When a fresh 1d8 is actually
rolled this call (`new`/`reroll`, or persistence breaking), the
description reads:

```
Unnatural stillness
🎲 1d8 (8) = 8

The wind stops and birds fall silent. ...
```

— the weather name is bold on its own line, the roll notation sits
plain on the line below it, then a blank line before the flavor text.
`show`, `set`, and a held persistence result keep the older plain form
(`**8. Unnatural stillness**` followed directly by the flavor text)
since no 1d8 was rolled that call.

## Artwork

Six of the eight results have a thumbnail, pulled from the shared
[`images/`](../../../images) folder via `raw.githubusercontent.com` URLs
(see `THUMBS` in `weather.alias`):

| Roll | Weather | Thumbnail |
| --- | --- | --- |
| 1 | Clear skies | `clear-skies-thumb.webp` |
| 2 | Low river mist | `low-river-mist-thumb.webp` |
| 3 | Steady drizzle | — none yet |
| 4 | Hard wind | `hard-wind-thumb.webp` |
| 5 | Passing showers | `passing-showers-thumb.webp` |
| 6 | Cold, soaking rain | `cold-soaking-rain-thumb.webp` |
| 7 | Thunderstorm | — none yet |
| 8 | Unnatural stillness | `unnatural-stillness-thumb.webp` |

No banner image is used for any result — Discord fixes the embed's
width and the thumbnail's position regardless, so a banner only added
vertical height without fixing text wrapping. Add entries to `THUMBS`
the same way as new art is produced (results 3 and 7 are still
outstanding).
