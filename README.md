# ETTOKEN-Cryptocurrency
Build your own cryptocurrency using ERC-20 tokens

Let's break it down line-by-line and understand what is going on:

=> ***pragma solidity ^0.8.0;***

This line specifies the compiler version of Solidity to be used. ^0.8.0 means any version greater than 0.8.0.

=> ***import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol";***

This line imports the ERC-20 token standard from OpenZeppelin (OZ). OZ is an Ethereum security company. Among other things, OZ develops reference contracts for popular smart contract standards which are thoroughly tested and secure. Whenever implementing a smart contract which needs to comply with a standard, try to find an OZ reference implementation rather than rewriting the entire standard from scratch.

=> ***contract EnesTektasToken is ERC20 {
    ...
}***

This specifies a new contract, named ETToken, in our Solidity file. Also, it says that this contract is an instance of ERC20. ERC20 in this case refers to the standard contract we imported from OpenZeppelin.

=> ***constructor(string memory _name, string memory _symbol) ERC20(_name, _symbol) {
     ...
}***


Essentially, we created constructor function that is called when the smart contract is first deployed. Within the constructor, we want two arguments from the user - _name and _symbol which specify the name and symbol of our cryptocurrency. E.g. name = Bitcoin, symbol = BTC.

What happens after it is more interesting. Immediately after specifying the constructor function, we call ERC20(_name, _symbol).

The ERC20 contract we imported from OpenZeppelin has its own constructor, which requires the name and symbol parameters. Since we are extending the ERC20 contract, we need to initialize the ERC20 contract when we deploy ours. So, as part of our constructor, we also need to call the constructor on the ERC20 contract.

Therefore, we are providing _name and _symbol variables to our contract, which we immediately pass on to the ERC20 constructor, thereby initializing the ERC20 smart contract.

=> ***_mint(msg.sender, 100 * (10**18));***

_mint is an internal function within the ERC20 standard contract, which means that it can only be called by the contract itself. External users cannot call this function.

Since you as the developer want to receive some tokens when you deploy this contract, we call the _mint function to mint some tokens to msg.sender.

_mint takes two arguments - an address to mint to, and the amount of tokens to mint

msg.sender is a global variable injected by the Ethereum Virtual Machine, which is the address which made this transaction. Since you will be the one deploying this contract, your address will be there in msg.sender.

10 * 10 ** 18 specifies that you want 10 full tokens to be minted to your address.
