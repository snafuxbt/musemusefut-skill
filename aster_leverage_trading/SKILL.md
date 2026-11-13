# Aster Leverage Trading

For the full setup walkthrough — including the agent-run setup where
the agent creates the wallet, the agent key, and the deposit — see
`SETUP.md` in the repository root.

## Set up the account before you trade

- Trade on Aster, a perpetual futures DEX on BSC, using the account holder's own wallet and their own USDT.

- Deposit USDT to the Aster vault contract (0x128463A60784c4D3f46c23Af3f65Ed859Ba87974) with broker 0 for futures, after approving the USDT spend from the wallet, and verify the vault address against Aster's current documentation before the first deposit.

- Approve a separate agent key from the main wallet with an EIP-712 signature, and give that key perpetual-trading permission only, never withdrawal permission.

- Keep the main wallet key out of the agent's reach: the agent trades only with the agent key, and the main key signs the approval once and is never used again.

- Switch the account from Multi-Assets mode to Single-Asset mode before placing an isolated order, because isolated margin is rejected while Multi-Assets mode is on.

- Use the Aster public API at https://fapi.asterdex.com for prices, klines, and account data.

- Never write a private key, seed phrase, password, token, or card number into this skill, a prompt, a chat message, or any shared file.

## Size the trade before you place it

- Use isolated margin only and never use cross margin for a leveraged trade.

- Use 5x to 10x leverage as the default and treat 100x only as a venue ceiling that you never use as a default.

- Check the minimum quantity, the minimum order value, the tick size, and the exchange price band before you choose a coin, and record them with the entry price.

- Reject an entry that sits outside the price band (about 3 percent from the mark price) and move the entry inside the band, still inside the retest zone, instead of forcing the original price.

- Calculate notional as quantity multiplied by entry price and calculate required margin as notional divided by leverage.

- Compare required margin with free margin before you place the order and skip the coin when the minimum quantity forces leverage above the level you intended.

- Remember that a 0.001 BTC minimum quantity is about 76 dollars of notional near a 76000 dollar price, so on a small margin it can force leverage far above the plan — check the forced leverage before you place the order.

- Check the estimated liquidation price before you place the order and skip the trade when liquidation sits closer than the stop loss.

## Screen and rank candidates

- Screen the full USDT perpetual universe on Aster and keep only pairs with 24 hour volume above 5 million dollars and technical levels you can verify from a live source.

- Skip a coin when it has no verifiable setup of its own and when it only follows another coin or when its volume on Aster is small.

- Skip a coin when daily volatility is too wide for the account size or when it is range bound with no clear resistance or support level.

- Use a limit entry at a retest of broken support for a short setup and wait for price to reach that zone instead of shorting at the current price.

- Prefer a reward to risk ratio near 3 to 1, accept 2.5 to 1 as the floor, and treat a lower ratio as a weaker candidate that stays in the queue.

- Rank candidates by reward to risk and place the highest ranked trade first and queue the rest until capital frees up.

- Check the macro calendar for a scheduled release on the entry day and treat a limit fill around that release as spike risk because the stop loss only becomes active after the fill.

- Leave a trade unplaced when no candidate passes the volume, level and reward to risk checks instead of forcing a trade to keep a position open.

## Place, monitor and exit

- Place a limit order only and record entry, stop loss, take profit, quantity, notional, margin, reward to risk, liquidation estimate, order id and snapshot time.

- Attach the stop loss and take profit when the order fills and use a monitor that checks fills at least every five minutes.

- Execute a stop loss or take profit automatically when it is hit and report the result after the execution instead of asking first.

- Never move a take profit or stop loss because of a casual remark about a level; change one only on a clear instruction or a documented change in the analysis.

- Cancel an unfilled order that locks margin needed for a better ranked trade and recheck free margin before you place the replacement.

- Keep only one live capital plan at a time and do not place a queued trade until a filled trade closes or an unfilled order is cancelled.

- Roll realised profit into the next setups so positions grow with the account, but keep every trade sized on its own with its own stop loss, and never go all-in on one position.

## Report and learn

- Report only the result after an execution and include the fill price, the exit price and the realised profit or loss.

- Write a post-mortem for every closed trade: what the structure and the retest did, and whether a loss came from news or from a bad read.

- Treat a win as no proof that the setup was good and a loss as no proof that it was bad; judge the process, not the outcome.

- Watch BTC as the market leader and report a strong bounce that threatens open shorts with the data and the two options (hold and trust the stops, or close early to lock profit), without acting on your own.

## Hard limits

- Never trade without a stop loss, never use cross margin, and never go all-in on one position.

- Never chase price with a market order and never raise leverage above the plan only because a minimum quantity forces it.

- Never promise profit and never present a floating profit as realised.

- Never use a private key, seed phrase, or main wallet credential inside the agent; the agent trades only through its own limited agent key.
