# Building-on-Avalanche: Degen Token(ERC-20)
This Solidity smart contract creates a custom ERC20 token and deploy it on the Avalanche network for Degen
Gaming. The following functionality: Minting, Transffering, Redeeming, Checking balance, and Burning tokens. 

## Description
This code will explain on how to Create ERC-20 token and Deployit on the Avalanche network for Degen Gaming.
## Getting Started
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

Your task is to create a ERC20 token and deploy it on the Avalanche network for Degen Gaming. The smart contract should have the following functionality:

Minting new tokens: The platform should be able to create new tokens and distribute them to players as rewards. Only the owner can mint tokens.
Transferring tokens: Players should be able to transfer their tokens to others.
Redeeming tokens: Players should be able to redeem their tokens for items in the in-game store.
Checking token balance: Players should be able to check their token balance at any time.
Burning tokens: Anyone should be able to burn tokens, that they own, that are no longer needed.

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract DegenToken is ERC20 {
    address public owner;

    event TokensMinted(address indexed recipient, uint256 amount);
    event TokensTransferred(address indexed from, address indexed to, uint256 amount);
    event TokensRedeemed(address indexed player, uint256 amount);
    event TokensBurned(address indexed owner, uint256 amount);

    constructor(string memory name, string memory symbol, uint256 initialSupply) ERC20(name, symbol) {
        owner = msg.sender;
        _mint(msg.sender, initialSupply);
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Ownable: caller is not the owner");
        _;
    }

    function mint(address account, uint256 amount) external onlyOwner {
        _mint(account, amount);
        emit TokensMinted(account, amount);
    }

    function transfer(address recipient, uint256 amount) public virtual override returns (bool) {
        _transfer(_msgSender(), recipient, amount);
        emit TokensTransferred(_msgSender(), recipient, amount);
        return true;
    }

    function redeemTokens(uint256 amount) external {
        require(balanceOf(msg.sender) >= amount, "Insufficient balance");
        _burn(msg.sender, amount);
        emit TokensRedeemed(msg.sender, amount);
    }

    function checkBalance(address account) external view returns (uint256) {
        return balanceOf(account);
    }

    function burn(uint256 amount) external {
        require(balanceOf(msg.sender) >= amount, "Insufficient balance");
        _burn(msg.sender, amount);
        emit TokensBurned(msg.sender, amount);
    }
}


   
        
## Executing Program
To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/. 
Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension 
(e.g., HelloWorld.sol). Then copy the code given in the assessment.

## Author
Julian Caster Troy Lopez
BSIT
National Teachers College
