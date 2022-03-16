# Metalifes Cross Chain Swap

## Overview
BSC AURORA Swap Contracts are responsible for registering swap pairs and swapping assets between BSC and AURORA.

![](./assets/bsc-aurora-swap.png)

### Register swap pair

1. Users register swap pair for bep20 token on BSC via BSCSwapAgent(`createSwapPair`) if token is not registered.
2. Swap service will monitor the `SwapPairRegister` event and create swap pair on AURORA: 
    
    1. create an ERC20 token on AURORA
    2. record the relation between bep20 token and erc20 (AURORA) token.

### Swap from BSC to AURORA

Once swap pair is registered, users can swap tokens from BSC to AURORA.

1. Users call `swapBSC2ERC` via BSCSwapAgent and specify bep20 token address, amount and swap fee.
2. Swap service will monitor the `SwapStarted` event and call `fillBSC2ERCSwap` via BSCSwapAgent to mint corresponding erc20 (AURORA) tokens to the same address that initiate the swap.

### Swap from AURORA to BSC

Once swap pair is registered, users can swap tokens from AURORA to BSC.

1. Users call `swapERC2BEP` via AURSwapAgent and specify erc20 token address, amount and swap fee. Erc20 tokens will be burned.
2. Swap service will monitor the `SwapStarted` event and call `fillERC2BEPSwap` via AURSwapAgent to transfer corresponding bep20 tokens to the same address that initiate the swap.
