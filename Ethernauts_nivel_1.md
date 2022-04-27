## Level 1 Fallback

Un gusto tenerte por aqui, sigamos con nuestro camino para ser desarrolladores web3.0, en esta entrada vamos a continuar con ethernaut, en este primer nivel ya vamos a poder interactuar directamente con el contrato inteligente, por lo que nuestro primer paso será observar que nos ofrece.
 
En las instrucciones del contrato tenemos las siguientes pistas:
  
- Sending transactions using web3.js to a contract and to a payable function
- Conversion between units ether & wei
- Solidity contract fallback function 

Para este nivel, necesitaremos una cantida de ether de prueba y la interacción con la terminal de nuestro navegador.
  
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

import '@openzeppelin/contracts/math/SafeMath.sol';

contract Fallback {

  using SafeMath for uint256;
  mapping(address => uint) public contributions;
  address payable public owner;

  constructor() public {
    owner = msg.sender;
    contributions[msg.sender] = 1000 * (1 ether);
  }

  modifier onlyOwner {
        require(
            msg.sender == owner,
            "caller is not the owner"
        );
        _;
    }

  function contribute() public payable {
    require(msg.value < 0.001 ether);
    contributions[msg.sender] += msg.value;
    if(contributions[msg.sender] > contributions[owner]) {
      owner = msg.sender;
    }
  }

  function getContribution() public view returns (uint) {
    return contributions[msg.sender];
  }

  function withdraw() public onlyOwner {
    owner.transfer(address(this).balance);
  }

  receive() external payable {
    require(msg.value > 0 && contributions[msg.sender] > 0);
    owner = msg.sender;
  }
}
```

Consultando la terminal podemos observar que tenemos las mismas instrucciones que en el nivel cero 
  
Tenemos que en las instrucciones debemos obtener el control del contrato y hacer un retiro de todos los fondos del contrato. 

Contamos con dos funciones fallback en el contrato que nos pueden servir `contribute` y `receive`.
Primero notemos que para obtener dicho control, de acuerdo con el contrato inteligente, tenemos tres posibilidades
