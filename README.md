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

### Day 2

I felt the hardest part of this puzzle was parsing the each line of text into a data structure I could work with.

I knew I wanted to use a Keyword list and ended up calling `String.split` more than I would have liked:

```elixir
def parse(input) do
  input
  |> String.split("\n", trim: true)
  |> Enum.map(fn str ->
    [k, v] = String.split(str, ":", trim: true)

    key =
      k
      |> String.split(" ", trim: true)
      |> (fn [_, n] -> n end).()
      |> String.to_integer()

    value =
      v
      |> String.split(";", trim: true)
      |> Enum.map(&String.split(&1, ",", trim: true))
      |> List.flatten()
      |> Enum.map(fn x ->
        x
        |> String.trim()
        |> String.split(" ")
        |> (fn [n, color] -> {String.to_atom(color), String.to_integer(n)} end).()
      end)
      |> List.flatten()

    {key, value}
  end)
end
```
