# RustPoker

[![Build Status](https://travis-ci.org/kmurf1999/rust_poker.svg?branch=master)](https://travis-ci.org/kmurf1999/rust_poker)
[![docs.rs](https://docs.rs/rust_poker/badge.svg?version=0.1.3)](https://docs.rs/rust_poker)

Fast range vs. range equity calculation for poker written in rust

 - [Crates.io](https://crates.io/crates/rust_poker)

## Hand Evaluator
 - Evaluates hands with any number of cards from 0 to 7
 - Higher score is better

### Usage

```rust
use rust_poker::hand_evaluator::{Hand, CARDS, evaluate};
// cards are indexed 0->51 where index is 4 * rank + suit
let hand = Hand::empty() + CARDS[0] + CARDS[1];
let score = evaluate(&hand);
```

## Equity Calculator
 - Runs a multithreaded monte-carlo simulation to calculate range vs range equities
 - Supports up to 6 players

### Usage

```rust
use rust_poker::hand_range::{HandRange, get_card_mask};
use rust_poker::equity_calculator::calc_equity;
let ranges = HandRange::from_strings(["AK,22+".to_string(), "random".to_string()].to_vec());
let public_cards = get_card_mask("2h3d4c".to_string());
let n_games = 10000;
let n_threads = 4;
let equities = calc_equity(&ranges, public_cards, n_threads, n_games);
```

# Credit

The hand evaluator and equity calculator library is a rust rewrite of **zekyll's** C++ equity calculator, [OMPEval](https://github.com/zekyll/OMPEval)
