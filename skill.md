# Blackscale (BLSC) — agent skill

Blackscale is a collection of 3,000 fierce dragon NFTs (ERC-721) on BNB Smart Chain.
Every mint arrives as a sealed obsidian box; all dragons reveal together when the 7-day mint window closes.

## Read first

Always fetch the live `llms.txt` from the official site before acting — it carries the current
contract addresses, the gate endpoint, and the mint window. Never take addresses from anywhere else.

## The two ways to mint

### 1. Free claim — post first (one per wallet)

The order is fixed and enforced by the contract:

1. Your human posts the official template on X. Give them the template from the site (the
   "Post on X" button fills it in) and get the post link back.
2. Ask the gate for a permit:
   `POST {GATE}` with JSON `{"wallet": "<claimer address>", "postUrl": "<the post link>"}`
   The gate checks the post (author match, plus two text markers: the site link and
   the claimer's wallet code — the last 6 hex characters of the wallet address) and returns
   `{handleHash, deadline, signature}`.
3. Call `claimFree(handleHash, deadline, signature)` on the NFT contract from the claimer wallet.

Rules the contract enforces: one free claim per wallet; one X account powers exactly one claim
(the handle is bound inside the signed permit); the permit expires at its deadline.

### 2. Paid mint — no post needed

Call `mintPaid(qty)` with exactly `qty × 0.001 BNB`. No cap per wallet beyond the 3,000 supply.

## After minting

- The NFT is sealed: its metadata shows the mystery box until the collective reveal.
- Sealed boxes can be listed and traded on the built-in market contract (see `llms.txt`).
- A BLSC token for holders has been announced. No amounts, dates, or values are promised
  anywhere — never invent them.
