## Repository

https://github.com/sherlock-audit/2023-06-dinari

## Report

https://audits.sherlock.xyz/contests/98/report 

## Key Points

- Bridge Assets: Assets/tokens which are cross blockchain

## Contracts

| Contract | Summary |
| --- | --- |
| BridgedERC20.sol | The ERC20 token to represent bridged assets. In the contract, there is a mechanic to restrict certain addresses from sending and receiving tokens called transferRestrictor. |
| TransferRestrictor.sol | Does some basic logic for blacklisting and whitelisting address. |
| OrderFees.sol | A helper contract to calculate fees and do math. |
| OrderProcessor.sol | The abstract contract which handles ording logics. Including request, fill, and cancel orders. Each operation has a virtual internal function to be implemented by implementation contracts. |
| BuyOrderIssuer.sol | Handles the logic for buying bridge tokens. When orders are filled, a new token will be minted. When orders are canceled, sends the fees (if applicable) to the treasury, and transfer the escrows to the recipient.   |
| DirectBuyIssuer.sol | Handles the direct payment when purchasing orders. Now there are functions to take and return escrows, but can only be called by operator role. |
| SellOrderProcessor.sol | Handles the sell operation for bridge assets. Does the similar things as the above contracts, but it sells instead. |

## Findings

None😭

I actually accidentally saw one of the high risk finding on the report, and it was about that the `BridgeERC20` contract does not check for restricted address when minting or burning.

## Lessons Learned

1. When there is access control, are the access controls applied for all possible operations?
2. Stock split is a new concept, maybe think about those really edge-cases when doing audits.
