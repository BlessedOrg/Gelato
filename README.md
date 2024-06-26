# Blessed Gelato.networks Feedback

## Introduction

Welcome to the GitHub repository for Blessed experience with Gelato.Networks, a onchain ticketing solution developed during our participation in the Infinite Space Bazaar Hackathon. 
This document provides an overview of our experience during the hackathon, and the key findings and lessons learned using Gelato.networks.

## Project Overview

### Project Name: Blessed

Blessed is an innovative ticketing solution designed to streamline the process of event ticketing, enhance user experience, and provide robust features for event organizers.

### Tech Stack

During the hackathon, we utilized a new tech stack to build Blessed, which includes:

- **Frontend**: React
- **Backend**: Node.JS 
- **Database**: PostGreSQL
- **Network**: Gelato OP Celestia  
- **Other Tools**: Gelato.networks RaaS, Thirdweb, OpenZepplin 

## Hackathon Experience

### Team Members

- Adam - Full Stack (including Solidity)
- Alex - Designer - UX / UI
- Alper - Art Director / Branding & UX UI
- Artur - Solidity / Architecture
- Daud - Product - UX / UI
- Filip - Full Stack 
- Viet - Visionary & Lead Architect

### Goals

- Develop a onchain fair and entertaining ticketing solution within the hackathon timeframe.
- Explore and implement the new tech stack.
- Ensure the application is scalable, user-friendly, and secure.

### Findings that might help others

1. **Challenge 1**: VRF and Whitelist  
   **Solution**: When we started we were trying to access https://app.gelato.network/vrf?chainId=123420111 but fugured out due to the help of Gelato by providing the contract and we assume it needed to be whitelisted. So maybe mention that in your VRF docs. 

2. **Challenge 2**: Problem with the Modulo Operator
When randomNumber is a multiple of eligibleParticipants.length - j, the result of the modulo operation will be 0:
```
uint n = j + (randomNumber % (eligibleParticipants.length - j));
```
Example
For instance, if randomNumber is 20 and eligibleParticipants.length - j is 5:
```
randomNumber % (eligibleParticipants.length - j) = 20 % 5 = 0
```
In this case, n would always be j, meaning no effective randomness is added, and no participant positions are swapped.

**Solution**: 
To address this issue, one possible solution is to ensure that randomNumber is better distributed and not just a static value.  

3. **Challenge 4**: Using Account Abstraction of Thirdweb and Gelato relay.  
 **Solution**: Check if we sign off with Thirdweb works and then it was fine.  

4. **Challenge 5**: Error using the SDK for adding a new task to the VRF  
   Codesnippet that caused it: 
```solidity

const functionSignature = '_fulfillRandomness(uint256,uint256,bytes)';
const functionSelector = ethers.utils.keccak256(ethers.utils.toUtf8Bytes(functionSignature)).slice(0, 10);
const params = 
{name: taskName || `VRF task ${new Date().toISOString()}`,
    execAddress: contractAddr,
    execSelector: functionSelector,
  }
const { taskId, tx } = await gelatoAutomate.createTask(params as any);

```

Error Message

```
 "cannot estimate gas; transaction may fail or may require manual gas limit
 [ See: https://links.ethers.org/v5-errors-UNPREDICTABLE_GAS_LIMIT ]
(error={\"reason\":\"execution reverted: Automate._validModules:
PROXY is required\",\"code\":\"UNPREDICTABLE_GAS_LIMIT\",\"method\":\"estimateGas\",\"transaction\":{\"from\":\"0x727b6D0a1DD1cA8f3132B6Bc8E1Cfa0C04CAb806\",\"maxPriorityFeePerGas\":{\"type\":\"BigNumber\",\"hex\":\"0x59682f00\"},\"maxFeePerGas\":{\"type\":\"BigNumber\",\"hex\":\"0x59682f64\"},\"to
```
**Solution**:
Just simply add **dedicatedMsgSender: true**, to the params and it will stop complaining about PROXY



**Challenge 6**: Temporary lagging network at various times   
**Solution**: As we were uanble to deploy contracts we informed support. 


