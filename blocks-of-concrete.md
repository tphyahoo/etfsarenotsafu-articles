*[Freestanding idea, not yet slotted into the series. Rough draft for ongoing noodling.]*

# Blocks of Concrete: A Custody Model You Don't Need a Cryptography Degree to Audit

## The proposal

Take a hardware wallet — a Trezor, say. Don't touch the electronics. Just run its I/O — the two buttons, the screen — out on a cable to the surface of an arbitrarily large block of poured concrete, and then bury the wallet itself dead center in the middle of that block as it cures. The interface to the outside world is a cable end sticking out of a slab. Everything else is rock.

That's the whole idea. It sounds almost too dumb to be a real proposal, which is exactly the point.

## Why the dumbness is the feature

Every custody model this series has spent several pieces picking apart — MPC quorums, threshold signatures, audited-crypto-but-undisclosed-policy-layers — has the same underlying property: verifying it requires trusting someone else's expertise. You can't personally check whether Coinbase's `cb-mpc` implementation is sound. You can't personally verify a quorum configuration you've never seen. Even a Cure53 audit is you trusting Cure53, who you're trusting to have done a good job, reporting on a system you still can't independently inspect. The whole stack is opaque by necessity — that's what "cryptographic" and "policy layer" mean in practice: things happening in a place you can't see, checked by people you have to take on faith.

A block of concrete has none of that problem. Its security properties are: how big is it, how much does it weigh, and is it still where it was yesterday. A twelve-year-old can reason about all three. There's no protocol to understand, no firm to trust, no audit to read — just mass, and whether the mass moved. That's not a lesser security model than MPC. It's a *legible* one, which almost nothing else in this entire industry is.

## What it actually defends against

Be precise about the threat model, because this doesn't replace everything — it replaces one specific, underrated risk: **quiet, fast, undetected physical access to the signing device.** An insider with legitimate facility access could swap a wallet, clone it, or walk off with it during a maintenance window. That's a real, boring, non-cryptographic failure mode — arguably closer to how most real-world custody failures actually happen than any MPC bug ever has. A wallet root-cast into a few tons of concrete can't be swapped, cloned, or walked off with quietly. Getting it out means a jackhammer, a demolition saw, or a thermal lance, on-site, for hours, making a great deal of noise and mess, in front of whatever cameras, coworkers, or passersby happen to exist. It's not that it's impossible to defeat. It's that defeating it is *conspicuous by construction* — the opposite of every insider-threat scenario this series keeps circling back to, where the whole danger is that nobody notices until the money's already gone.

What it does *not* defend against: someone with legitimate authorization walking up, pressing the two buttons, and approving a transaction they shouldn't. That's still a policy/authorization problem, not a physical one — concrete protects the box, not the decision to use it. This is a complement to a real approval process (see: the BitMEX model, human sign-off, batch delays), not a substitute for one.

## Making the legibility literal

The fun part, and the part worth building out further:

- **Public placement, not hidden vaults.** The instinct with anything valuable is to hide it. This flips that: put it somewhere ordinary and visible — a parking garage, a lobby, wherever — precisely because the security doesn't depend on nobody knowing where it is. Everyone can know exactly where it is and it doesn't matter. That's a stronger claim than "we won't tell you where the HSMs are," and it's checkable in a way "trust our physical security" never is.
- **Publish the coordinates.** If it's genuinely this hard to move, there's no cost to disclosing exactly where it sits. Anyone — a journalist, a competitor, a bored Bitcoiner with a drone — can go verify it's still there, still the same size, unmoved. That's a physical answer to the "proof of reserves" problem the rest of this series keeps running into: instead of a cryptographic signature nobody can check, a satellite photo anyone can check.
- **Timestamped proof-of-continued-existence**, borrowing the old "photograph it next to today's newspaper" trick — photograph the block next to a recent, verifiable timestamp (a block hash, a headline) at intervals, so "yes, still here, as of this morning" is a standing, cheap, repeatable claim rather than a one-time assertion.
- **Tamper-evidence baked into the pour.** Colored or marked aggregate, embedded mesh, whatever — something that makes a patched, repaired breach visually obvious rather than invisible. A cracked-and-repatched slab should look nothing like an undisturbed one.
- **Scale it as real multisig, not a single point of failure.** One giant block is a fun thought experiment but a bad architecture — one location, one flood/earthquake/jurisdiction away from a bad time. The actual version of this is k-of-n: several smaller blocks, geographically distributed, each holding one key share, so no single slab (or city, or country) is a single point of failure. This is just concrete-flavored collaborative custody — the same idea as Unchained or Casa, with a physical-legibility twist instead of a purely cryptographic one.

## The honest weaknesses

- Concrete is not literally indestructible — given enough time, tools, and lack of oversight, it can be breached. The security model is "slow and conspicuous," not "impossible."
- Electronics degrade. Batteries die. A wallet cast in concrete for a decade needs a maintenance plan (accessible battery compartment via the same cable channel, or a planned rotation schedule into a fresh pour) or it becomes a very expensive, very secure brick.
- This is a personal/small-institution-scale idea as described. Whether it scales to "custody for a $90B ETF" is an open question. Probably yes in spirit — bigger blocks, more of them, real k-of-n. But the operational details need actual design work, not just "more concrete": who presses the buttons, how withdrawal requests get physically routed to the right block, audit logging of physical access attempts.

## Prior art

Not claiming originality here, and no objection if someone else wants to spend $100k getting this through a patent office.

**The well-documented industrial precedent**: FIPS 140-2 Level 3/4 hardware security modules already use a technique called **potting** — encasing the actual circuit board in hard, opaque epoxy resin, so that physically extracting the chip is inherently destructive and leaves obvious evidence. That's the same underlying principle — make removal destructive and visible, not just difficult — at component scale. It just lacks the public-legibility angle this idea adds: there's no "publish the coordinates" equivalent for a potted chip sitting inside a locked data center rack.

**The likely actual origin, unconfirmed**: the author recalls encountering this idea via a shitpost comment on Mircea Popescu's Trilema blog or its associated IRC channel (part of the "tmsr"/The Most Serene Republic community). It was originally proposed for a PGP signing device, not a Bitcoin wallet, though the logic transfers directly. A search turned up circumstantial support but not the original source: a March 2017 IRC log has `asciilifeform` (Stanislav Datskovskiy, a figure in that community known for advocating physically robust, non-networked approaches to key security, and the builder of the FG hardware TRNG) telling Mircea Popescu, *"mircea_popescu is stingy re the concretes, and asciilifeform likes concretes"* — which suggests "concretes" was a real, recurring bit in that community, plausibly this exact idea. The original post or exchange itself wasn't located. `btcbase.org`'s IRC log search (which indexes the tmsr/Trilema archives far more thoroughly than general web search) is the better tool for tracking down and properly crediting the actual source, if that matters later.

## Where this might go

This is presented at the pure concept stage — a genuinely interesting instinct (physical legibility as an answer to cryptographic opacity) that could become a real appendix or sidebar to the "WTF to Do" prescriptive piece, once it's had more time to develop. Rough open questions for future noodling: does this want a catchy name? Is there a minimum viable prototype worth actually building and photographing? Is there prior art worth citing (bank vault time-locks, seed-phrase steel plates like Cryptosteel/Blockplate, or the various "bury it in the backyard" cold-storage folklore) that this should be positioned against rather than presented as wholly novel?
