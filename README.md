Guessing Game — DS210 Project 1

A number guessing game written in Rust where the computer tries to guess a number you picked. The core idea is to implement and compare different guessing strategies — from a dumb random guesser to an optimal one — and then run experiments to see how they actually perform.


How it works

You pick a number between 0 and 16, write it down so you don't cheat yourself, and the program tries to guess it by asking yes/no questions. The interesting part is how it chooses what to guess — that's the strategy.

The repo comes with two example strategies to show the structure:


BadStrategy — asks if the number is min, then jumps straight to max - 1. Absolutely terrible, but it compiles.
RandomStrategy — keeps guessing randomly until it hits. Also terrible, but in a more chaotic way.

Running the game

To play with the random strategy (just to see how it works):

bashcargo run --bin game -- --strategy random

To test your own implementations:

bashcargo run --bin game -- --strategy part1
cargo run --bin game -- --strategy part2


Testing

Parts 1 and 2 are tested manually by running the game. For part 3, there's an actual test suite:

bashcargo test --bin game -- --test-threads 1

If you want to isolate specific test groups instead of running everything at once:

bashcargo test --bin game bad_strategy -- --test-threads=1
cargo test --bin game part1 -- --test-threads=1
cargo test --bin game part2 -- --test-threads=1

Running with --test-threads 1 keeps the output readable — parallel test output gets messy fast.


Experiments (Part 4)

After finishing part 3, you can run the experiment binary to benchmark how different strategies compare across many trials. It outputs a plot to plot.png:

bashcargo run --bin experiment


Notes


Don't touch any files outside of part1.rs, part2.rs, and part3.rs. The autograder only looks at those three files and ignores everything else.
The Player struct in player.rs handles tracking guesses — your strategy just needs to implement the Strategy trait and call player.ask_if_equal().
The optimal strategy for a range of size N should find the number in at most ⌈log₂(N)⌉ guesses. The random strategy... will not do that.
Follow the instructions on gradescope. **Make sure you submitted the correct file for each part!**
