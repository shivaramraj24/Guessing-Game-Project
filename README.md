# Guessing Game — DS210 Project 1

A number guessing game written in Rust where the *computer* tries to guess a number *you* picked. The core idea is to implement and compare different guessing strategies — from a dumb random guesser to an optimal one — and then run experiments to see how they actually perform.

---

## How it works

You pick a number between 0 and 16, write it down so you don't cheat yourself, and the program tries to guess it by asking yes/no questions. The interesting part is *how* it chooses what to guess — that's the strategy.

The repo comes with two example strategies to show the structure:

- **BadStrategy** — asks if the number is `min`, then jumps straight to `max - 1`. Absolutely terrible, but it compiles.
- **RandomStrategy** — keeps guessing randomly until it hits. Also terrible, but in a more chaotic way.

Your job (parts 1–3) is to implement strategies that actually work well.

---

## Project structure

```
├── game.rs          # main game loop + CLI
├── player.rs        # Player struct that tracks guesses and answers
├── strategies.rs    # BadStrategy and RandomStrategy (provided examples)
├── part1.rs         # your solution for part 1
├── part2.rs         # your solution for part 2
├── part3.rs         # your solution for part 3
├── experiment.rs    # runs experiments and generates a performance plot
└── Cargo.toml
```

---

## Running the game

To play with the random strategy (just to see how it works):

```bash
cargo run --bin game -- --strategy random
```

To test your own implementations:

```bash
cargo run --bin game -- --strategy part1
cargo run --bin game -- --strategy part2
```

---

## Testing

Parts 1 and 2 are tested manually by running the game. For part 3, there's an actual test suite:

```bash
cargo test --bin game -- --test-threads 1
```

If you want to isolate specific test groups instead of running everything at once:

```bash
cargo test --bin game bad_strategy -- --test-threads=1
cargo test --bin game part1 -- --test-threads=1
cargo test --bin game part2 -- --test-threads=1
```

Running with `--test-threads 1` keeps the output readable — parallel test output gets messy fast.

---

## Experiments (Part 4)

After finishing part 3, you can run the experiment binary to benchmark how different strategies compare across many trials. It outputs a plot to `plot.png`:

```bash
cargo run --bin experiment
```

---

## Notes

- **Don't touch any files outside of `part1.rs`, `part2.rs`, and `part3.rs`.** The autograder only looks at those three files and ignores everything else.
- The `Player` struct in `player.rs` handles tracking guesses — your strategy just needs to implement the `Strategy` trait and call `player.ask_if_equal()`.
- The optimal strategy for a range of size N should find the number in at most ⌈log₂(N)⌉ guesses. The random strategy... will not do that.
