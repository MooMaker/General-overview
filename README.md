# General-overview

MooMaker introduces framework for individual market makers to price CoW swap users through offchain signed bids. A designated CoW solver receives batch data and sends request to makers to swap particular tokens launching an offchain auction. During auction makers submit their EIP-712 signed bids and the best bid is displayed to solver as a solution which he may pick as the best one to pass to CoW driver.   

Purpose of MooMaker:

-Currently AMM pools are the main liquidity source to settle any unmatched orders on CoW. Settling with AMM protocols may not be optimal at times due to gas costs and limited locked liquidity in the pool. MooMaker gives an opportunity to settle cow batches using private liquidity which is likely to yield better prices on many occasions compared to AMMs

-Private liquidity may include proffesional market makers on centralized exchanges who have high fee tiers. Such players are normally able to provide very attractive prices to onchain traders due to their ability to effectively hedge each trade on their side

-Open offchain auction sparkles competition among market makers as they see every quote provided by each maker. This gives them the stimulus to outbid each other deriving the best possible price for cow user

Key components used: 

<img width="648" alt="image" src="https://github.com/MooMaker/General-overview/assets/105652074/3af55074-88a7-42f5-955c-cd588b76dfdd">


# Flow

1) Trader on CoW submits his limit order. If it is not matched with other trader, it is passed to solver through CoW driver to find the best available path to settle the trade.
2) Solver passes data on tokens that require swap to MooMaker offcahin service
3) Offchain service informs all connected market makers (MMs) about the batch that requires onchain settlement
4) MMs submit their EIP-712 signed bids through websocket to MooMaker offchain service
5) The best quote out of all provided is displayed to solver as the best solution that he may pick to offer CoW driver as a path
6) If accepted as the best solution, CoW driver will activate MooMaker smart contract swap function which will check validity of signed quote and execute swap by transfering tokens between the winning MM and CoW driver.

<img width="637" alt="image" src="https://github.com/MooMaker/General-overview/assets/105652074/8cdaffa2-3cee-47be-9645-08f0066b54db">


