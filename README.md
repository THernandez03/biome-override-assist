## Issue

[Go to the issue - biomejs/biome#6226](https://github.com/biomejs/biome/issues/6226)

### Context

This project demonstrates the structure and behavior of Biome configuration with overrides. The key components are:

- **`biome.json`** - The main Biome configuration file that defines formatting rules and override settings
- **`src/` folder** - Contains two example files:

  - `default-sorted.js` - A file that follows Biome's formatting rules and gets formatted correctly
  - `should-not-be-sorted.js` - A file that should be handled by the `overrides` configuration, but Biome still applies automatic formatting despite the specific override rules, highlighting a potential issue with the override functionality

- **`biome.unknown_key.json`** - An alternative Biome configuration file that I also tried to make it work, because based on the example on [the docs](https://next.biomejs.dev/reference/configuration/#overridesitemjson) I supposed that I can use any property to override. But unfortunately, this is recognized by biome as an invalid configuration keys (unknown `actions` key)

### Steps to reproduce the error

1. **Clone the repository**

```bash
git clone https://github.com/THernandez03/biome-override-assist
cd biome-override-assist
```

2. **Install dependencies**

```bash
bun install
```

3. **Execute the Biome format check**

```bash
bun check
```

This is the error that is actually throwing

```bash
» bun run check
$ biome check ./src
src/should-not-be-sorted.json:1:1 assist/source/useSortedKeys  FIXABLE  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  ✖ The keys are not sorted.

  > 1 │ {
      │ ^
  > 2 │         "x": true,
  > 3 │         "z": true,
  > 4 │         "a": true,
  > 5 │         "b": true,
  > 6 │         "d": true,
  > 7 │         "s": true
  > 8 │ }
      │ ^
    9 │

  ℹ Safe fix: They keys of the current object can be sorted.

    1 1 │   {
    2   │ - → "x":·true,
    3   │ - → "z":·true,
    4   │ - → "a":·true,
    5   │ - → "b":·true,
    6   │ - → "d":·true,
    7   │ - → "s":·true
      2 │ + → "a":·true,
      3 │ + → "b":·true,
      4 │ + → "d":·true,
      5 │ + → "s":·true,
      6 │ + → "x":·true,
      7 │ + → "z":·true
    8 8 │   }
    9 9 │


Checked 2 files in 1359µs. No fixes applied.
Found 1 error.
check ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  ✖ Some errors were emitted while running checks.


error: script "check" exited with code 1
```

### Expected behavior

```bash
» bun run check
$ biome check ./src
Checked 2 files in 1036µs. No fixes applied.
```
