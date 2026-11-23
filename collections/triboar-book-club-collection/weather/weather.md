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
effect, and (when rolled) the dice results.
