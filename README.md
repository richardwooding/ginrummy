# ginrummy

Pure-logic rules and scoring library for two-player Gin Rummy: meld
detection (optimal set/run partition), deadwood counting, knock/gin/undercut
scoring, lay-offs, and match play to 100.

Cards are plain ints 0..51: `Rank(c) = c % 13` (0=Ace .. 12=King, aces low),
`Suit(c) = c / 13` (0=♠ 1=♥ 2=♦ 3=♣). Everything is deterministic — no
randomness, no crypto, no networking — so callers can drive and verify games
reproducibly.

```go
deadwood, melds, unmatched := ginrummy.BestMelds(hand) // optimal partition
if ginrummy.CanKnock(hand) { // deadwood ≤ 10
	kPts, oPts := ginrummy.Score(knocker, opponent, ginrummy.IsGin(knocker))
	_ = kPts; _ = oPts
}
```

Compiles to WASM. Extracted from
[kibitz](https://github.com/richardwooding/kibitz), where it scores Gin Rummy
hands dealt via a dealerless mental-poker shuffle.

MIT licensed.
