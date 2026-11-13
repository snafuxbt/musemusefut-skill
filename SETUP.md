# Full Setup Guide: Aster Futures + Agent

From zero to a running agent — two paths: the agent does everything
(how we did it), or manual setup.

This guide contains **no private keys, seed phrases, or wallet
addresses belonging to anyone**. Everything here is steps and rules —
you use your own wallet and your own funds.

## Path 1 — The agent does everything, fully automatically (how we did it)

This is what actually happened in our setup. The user did **not**
create a wallet, did **not** register an account, and did **not**
deposit manually. All of it was done by the agent (Muse). The user
only provided capital and permission.

What the user did:

1. Provided capital: BNB in a Binance Agentic Wallet.
2. Gave permission: "you handle it" — the agent did the rest.

What the agent did:

1. Prepared the trading wallet (a new EVM wallet on BSC).
2. Created a separate agent key (not the main wallet key).
3. Approved the agent key from the trading wallet with an EIP-712
   signature — perpetual-trading permission only. The agent key
   cannot withdraw.
4. Swapped BNB into USDT, then transferred the USDT to the
   trading wallet.
5. Deposited the USDT to Aster futures (broker 0), using the
   deposit address from Aster's official documentation.
6. Switched the account to Single-Asset mode and set 10x
   isolated leverage.
7. Installed a monitor that checks every 5 minutes and reports
   results.

Someone else can get the same experience **if** their agent also
has a computer and tools like Muse: they only provide capital and
permission, and their agent does steps 1–7. Requirements: the
agent must have access to funds (a wallet it can use, for
example an Agentic Wallet) and permission to create the trading
wallet and the agent key.

If the agent **cannot** execute (for example a plain chatbot
without tools), use Path 2 below.

## Path 2 — Manual setup (if the agent cannot execute)

### A. Create a wallet

1. Install an EVM wallet from an official source: MetaMask, OKX
   Wallet, or Phantom (Chrome extension or mobile app, downloaded
   from each project's official site or official app store).
2. Create a NEW wallet. Write the seed phrase (12/24 words) on
   paper, store it offline, never photograph it and never save it
   on a phone or computer.
3. The seed phrase and private key are NEVER shared with anyone —
   not with the agent, not with a friend, not with any website.
4. Make sure the wallet can access BSC (BNB Smart Chain).
5. This is the MAIN wallet. Its key is used once to approve the
   agent key, and after that it is never used again by the agent.

### B. Fund it with USDT on BSC

1. Fund the wallet with USDT on BSC (BEP-20): buy on an exchange
   and withdraw to the wallet address (choose the BSC/BEP-20
   network), receive a transfer, or swap BNB into USDT on a DEX
   such as PancakeSwap.
2. Keep a little BNB in the wallet for gas (approval + deposit
   need BNB gas; the cost is small).
3. Decide your own capital size. Only use money you can afford
   to lose — never money you need.

### C. Deposit to Aster

Aster is a perpetual futures DEX on BSC: no KYC, wallet-only.
Minimum order $5 notional, taker fee 0.04%.

1. Connect the wallet to the Aster app/web (asterdex.com).
2. Deposit USDT to Aster futures (broker 0). Find the current
   deposit address in Aster's official documentation and verify
   it before your first deposit — never trust an address from a
   chat or a screenshot.
3. The flow: approve the USDT spend from the wallet first, then
   deposit. Once in, the USDT balance can be used to open long
   or short positions.
4. In the Aster account settings, make sure Single-Asset mode is
   active (not Multi-Assets), because isolated margin is rejected
   while Multi-Assets mode is on.

### D. Agent key

1. Create a SEPARATE key called the agent key. This is NOT the
   main wallet key — a new key used only for trading.
2. From the main wallet, sign an EIP-712 approval giving the
   agent key perpetual-trading permission ONLY. The agent key
   cannot withdraw funds.
3. After that, the trading agent uses the agent key. The main key
   stays safe and is never used again.
4. NEVER put a private key or seed phrase inside a prompt, a
   chat, or any shared file.

## What the agent still needs (beyond the skill)

The skill (`aster_leverage_trading/SKILL.md`) alone is not enough.
The agent also needs:

1. Access to funds (a wallet the agent can use, or an Agentic
   Wallet like the one we used).
2. The ability to create a trading wallet + agent key and sign
   the approval (Path 1). If it cannot, do Path 2 manually.
3. Access to the Aster API (`fapi.asterdex.com`) to read prices,
   place orders, and check positions.
4. A way to run a periodic monitor (checking about every
   5 minutes).
5. NEVER put a private key / seed phrase in a prompt or a chat.

## Risk (must be passed on)

- 10x leverage cuts both ways: liquidation sits only about 10%
  from entry.
- A stop loss can be gapped through when the market jumps on big
  news.
- Never use money you need. Never start big.
- Nothing guarantees profit — the only promise is the discipline
  of the rules.
