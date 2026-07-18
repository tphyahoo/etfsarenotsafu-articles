# Bitcoin ETFs Are Not Safu

How the Bitcoin behind America's spot ETFs is *actually* held — and where the reassuring language ("bank-grade," "multi-party," "proof of reserves," "qualified custodian") quietly stops meaning what you'd assume.

A five-part investigative series. **Work in progress — drafts shared for feedback; some footnotes are still being primary-verified.**

**Do not share yet unless you run by me first.** 

## In brief

The Bitcoin behind America's spot ETFs sits with a handful of custodians — overwhelmingly Coinbase. This series looks at how it's *actually* held, and finds the reassuring language doing a lot of quiet work.

**The custody is generic, not Bitcoin-native.** Bitcoin has its own on-chain way to share control of coins — multisig, which anyone can verify directly on the blockchain. Instead, Coinbase runs Bitcoin through the same complex, off-chain "multi-party computation" machinery it built for hundreds of other coins. Running one pipeline for everything is cheaper — but it means Bitcoin's security gets cross-contaminated with the needs of assets that don't deserve to be near it. But the contamination isn't that Bitcoin shares a custodian with other assets — a good custodian can hold many things well. It's that Bitcoin, the one asset with its own purpose-built custody, gets the generic machinery anyway, because it counts as one line item among hundreds. The fix isn't a cleverer machine: handle Bitcoin with Bitcoin's own tools, and break the pile into many small, capped, independent pieces — so that no single failure, and no single company, can lose it all.

**They audit the layer that was never the risk.** Custodians loudly publicize audits of their cryptography and stay quiet about the *policy layer* — the human process that decides who can actually move the coins. That layer, not the math, is where custodians have historically failed.

**And you can't check the reserves.** There's no mechanism to independently verify an ETF's Bitcoin against the blockchain — no published addresses, no watch-only key — and "proof of reserves," where it's offered at all, rarely means what it sounds like.

The series anchors on **Prime Trust**: a licensed, well-meaning custodian that collapsed — not from fraud, but from a boring operational detail nobody was watching. A bankruptcy judge later found even the Bitcoin "hopelessly commingled." Bitcoin is the one asset built to make ownership provably clear, and it still got mixed in with everything else.

The takeaway is simple. Institutions holding the public's Bitcoin should demand real segregation and real proof — cap it, distribute it, verify it — instead of trusting the brand. It matters most for the ETFs, which now sit on tens of billions of dollars of it. Bitcoin isn't a shitcoin. It's time custodians and their customers started acting like it.

## The series

1. [When Is a Fiduciary Not a Fiduciary? What FTX and Prime Trust Actually Broke](part1-fiduciary.md)
2. [Cross-Contamination: When Is Bitcoin Just Another Shitcoin?](part2-cross-contamination.md)
3. [When Is a Party Not a Party?](part3-party-not-a-party.md)
4. [When Is a Proof of Reserves Not a Proof?](part4-proof-of-reserves.md)
5. [Blocks of Concrete: A Custody Model You Don't Need a Cryptography Degree to Audit](blocks-of-concrete.md) — *in progress*

---

*"Safu" is crypto-community slang for "safe," from a 2018 Binance episode — often used ironically. The title is not reassurance. Feedback welcome.*
