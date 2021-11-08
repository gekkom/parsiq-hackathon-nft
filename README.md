# PARSIQ 101: Working With NFTs

## **[PARSIQ Portal Project Link](https://portal.parsiq.net/monitoring/projects/bcffcbb4-ea56-419b-969d-087ec1536a98/triggers)**

Normal ERC721 and ERC1155 NFTs can usually be monitored with already exsisting tools like the OpenSea API. But there are a lot of more exotic projects that require a custom solution to track. In this hackathon i will be using ParsiQL to monitor the [nftx](https://nftx.io/) smart contract, and log when new NFT vaults are created.

## The Contract
**AdminUpgradeabilityProxy:** `0xbe86f647b167567525ccaafcd6f881f1ee558216`

**NFTXVaultFactoryUpgradeable:** `0x6a911d2aaabe631f8d7daa82afbfe38633cb0dab`

***Some information on the contract:** Users deposit their NFT into an NFTX vault and mint a fungible ERC20 token (vToken) that represents a claim on a random asset from within the vault. vTokens can also be used to redeem a specific NFT from a vault.*

**1.** I got the abi of the smart contract.
![](https://i.imgur.com/OPTh9vi.png)

**2.** Uploaded it as json to the parsiq portal.
![](https://i.imgur.com/CgbBENu.png)

**3.** Selected the functions/events I needed in my smart triggers, selected my chain and named my user stream.
![](https://i.imgur.com/maJVEUx.png)

## Smart Triggers
**1.** The first trigger is watching the `createVault` function and outputting its parameters.
![](https://i.imgur.com/93q3LkQ.png)

**2.** In my other trigger i'm doing a similar thing with the `NewVault` event, which will give me the address of the newly created vault.
![](https://i.imgur.com/xqPBjcf.png)

***Note: I'm monitoring both the proxy and the actual contract because i couldn't find any information regarding proxy contracts in the PARSIQ docs.***

## Transport
Lastly i created a transport to output the data to google sheets and i configured that transport as a delivery channel in my triggers.
![](https://i.imgur.com/qZHMZJP.png)

**Google sheets:**

[NewVault output](https://docs.google.com/spreadsheets/d/1LWsfAryByOn-89FyhJu-uMv9IO6Jcp8ORNSTys_t9Gc/edit?usp=sharing)

[createVault output](https://docs.google.com/spreadsheets/d/1Oy5XsG-EyOjA7r4XF_YH6iIaCps2LFiUXgXebZRdF_M/edit?usp=sharing)

## Conclusion
It's incredibly easy to create custom monitoring solutions using PARSIQ and ParsiQL. In a few hours i was able to learn the platform and make smart triggres to track vault creation in the the [nftx](https://nftx.io/) smart contract.
