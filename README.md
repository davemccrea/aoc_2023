# Advent of Code 2024

My solutions in Elixir to Advent of Code 2023.

## Livebook

This year I decided to do everything in [Livebook](https://github.com/livebook-dev/livebook) combined with [KinoAOC](https://github.com/ljgago/kino_aoc) - it's a nice experience.

## Learnings

### Day 1

My tests passed but the answer I gave to AoC was not accepted. Turns out the Regex I had written did not account for two valid words sharing a character e.g. `eightwo`. I had to Google a lot but ended up using a positive lookahead assertion Regex. This is denoted by the `?=`:

```
~r/(?=(one|two|three|four|five|six|seven|eight|nine|[0-9]))/
```

