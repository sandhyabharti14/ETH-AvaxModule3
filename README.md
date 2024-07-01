# MyToken
=======

This Solidity program creates and manages a token by creating a smart contract. The contract has functionalities like total supply, balances, transferring tokens, and more.

## Description
-----------

This program is written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain. The contract has the following features:

* `mint`: Only the owner can mint new tokens and assign them to a specific address.
* `burn`: An address can burn (destroy) tokens from their own balance.
* `transfer`: A user can transfer tokens to another address.
* `approve`: A user can approve another address to spend tokens on their behalf.
* `transferFrom`: An approved address can transfer tokens from another address to a third address.

## Getting Started
---------------

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at <https://remix.ethereum.org/>.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., MyToken.sol). Copy and paste the following code into the file:
```solidity
pragma solidity ^0.8.0;

contract MyToken {
    string public name = "MyToken";
    string public symbol = "MTK";
    uint256 public totalSupply = 100 * 10**18; // 100 tokens with 18 decimals
    uint256 public decimals = 18;
    mapping(address => uint256) public balances;
    mapping(address => mapping(address => uint256)) public allowed;
    address public owner;

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);

    constructor() {
        balances[msg.sender] = totalSupply;
        owner = msg.sender;
    }

    function mint(address _to, uint256 _amount) public {
        require(msg.sender == owner, "Only the owner can mint tokens");
        balances[_to] += _amount;
        totalSupply += _amount;
        emit Transfer(address(0), _to, _amount);
    }

    function burn(uint256 _amount) public {
        require(balances[msg.sender] >= _amount, "Insufficient balance");
        balances[msg.sender] -= _amount;
        totalSupply -= _amount;
        emit Transfer(msg.sender, address(0), _amount);
    }

    function transfer(address _to, uint256 _amount) public {
        require(balances[msg.sender] >= _amount, "Insufficient balance");
        balances[msg.sender] -= _amount;
        balances[_to] += _amount;
        emit Transfer(msg.sender, _to, _amount);
    }

    function approve(address _spender, uint256 _amount) public {
        allowed[msg.sender][_spender] = _amount;
        emit Approval(msg.sender, _spender, _amount);
    }

    function transferFrom(address _from, address _to, uint256 _amount) public {
        require(balances[_from] >= _amount, "Insufficient balance");
        require(allowed[_from][msg.sender] >= _amount, "Insufficient allowance");
        balances[_from] -= _amount;
        balances[_to] += _amount;
        allowed[_from][msg.sender] -= _amount;
        emit Transfer(_from, _to, _amount);
    }
}

```
To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.0" (or another compatible version), and then click on the "Compile MyToken.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "MyToken" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it by calling the mint, burn, transfer, approve, and transferFrom functions. Now, provide the input for the functions and then click on "Transact" to get the output.

## Authors

Sandhya Bharti
bhartisandhya1411@gmail.com

## License

This project is licensed under the [MIT] License - see the LICENSE.md file for details
