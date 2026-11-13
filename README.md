# Aster Leverage Trading — Agent Skill

An agent skill for trading perpetual futures on [Aster](https://asterdex.com)
(a perp DEX on BSC) with isolated margin, disciplined sizing, and automatic
stop loss / take profit.

Built from a live account run by an AI agent: every rule here was
earned the hard way — including the sizing trap where a 0.001 BTC minimum
quantity forced leverage far above the plan.

## What's inside

- `aster_leverage_trading/SKILL.md` — the skill: account setup, sizing,
  screening, execution, monitoring, reporting, and hard limits.
- `aster_leverage_trading/skill.yaml` — skill metadata (name, description,
  category).
- `SETUP.md` — the complete setup guide: how the agent set everything
  up from scratch (wallet, agent key, deposit, monitor), plus the
  manual path if your agent cannot execute.

## Install

**Muse:** send the `aster_leverage_trading` folder to your agent and ask it
to save it as a skill named `aster_leverage_trading`. It will load
automatically for Aster futures work.

**Other agents:** paste the contents of `SKILL.md` as a system / project
instruction.

## The system in short

- Fully automatic: the agent sets everything up (wallet, agent
  key, deposit, monitor), runs the whole trading loop, and
  reports only results.
- Short the retest: broken support becomes the entry zone, limit orders only.
- 10x isolated margin, mandatory stop loss, reward:risk of at least 2.5:1.
- Minimum notional $5, 24h volume above $5M, price-band check before placing.
- TP/SL attached automatically on fill; a monitor re-checks every ~5 minutes.
- TP/SL execute automatically when hit; results are reported afterwards.
- Realised profit compounds into the next setups — but every trade is sized
  on its own, never all-in.
- Every closed trade gets a post-mortem: structure vs. news vs. bad read.

## What the agent still needs (beyond this skill)

1. Its own wallet + USDT on BSC, deposited to Aster (broker 0 = futures).
2. Its own agent key (perp-only, approved from the main wallet via EIP-712).
3. Access to the Aster API (`fapi.asterdex.com`) and a way to run a
   monitor on a schedule.

## Security

This repo contains **no private keys, seed phrases, wallet addresses, or
credentials of any kind**. Never add any to the skill, a prompt, or a chat.

## Risk

Leverage cuts both ways: at 10x, liquidation sits ~10% from entry, and a
stop loss can be gapped through on big news. Never trade money you need.
Nothing here promises profit — the only promise is the discipline of the
rules.
