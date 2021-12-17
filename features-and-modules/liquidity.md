# Liquidity

## What is the Liquidity Module?

The Liquidity Module ensures that there is a continuous supply of liquidity for both Fan Tokens and NFTs traded in the BitSong marketplace.

It is effectively the same type of model as used on decentralized exchanges like Uniswap. Token pools use automated market makers to determine a fair price, allowing anyone to swap any token for any other token for low, fixed fees. Liquidity providers can deposit their tokens into the pools to earn a share of fees paid by users.

However, the Liquidity Module offers some benefits over a standard AMM, by combining some of the more desirable features of an order book-based exchange. It uses a batch-based order book matching algorithm together with the AMM, offering more utility to a greater array of potential users.

The Liquidity Module redefines the concept of a “swap order” as it is in the AMM, to a “limit order with a short lifetime,” as it would be in an order book exchange. This model offers more freedom and flexibility on ways to provide liquidity. The combination of pool liquidity and limit order liquidity also provides users with a more enriched trading environment.

How does this work in practice? Let’s say Alice has acquired some of xArtist Fan Tokens. She can use the Liquidity Module to swap her xArtist Fan Tokens for BTSG, which she can then trade for other Cosmos ecosystem cryptocurrencies in Gravity DEX.

She could also choose to cash out to fiat currencies, using our integrated FIAT Bridge (IBAN connected to a [BTSG-supported Wallet](../btsg/wallets.md)).

(Please note that the first version of the Liquidity Module won’t support limit order options, but the code base structure anticipates and supports this as a feature expansion. This documentation will be updated as and when new features become available)
