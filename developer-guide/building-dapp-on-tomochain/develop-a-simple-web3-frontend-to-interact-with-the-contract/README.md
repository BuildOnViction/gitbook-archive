---
description: >-
  Now we’ve created the smart contract and deployed it to TomoChain blockchain
  (testnet). It’s time to create a UI so that people can use the shop!
---

# Develop a Simple Web3 Frontend to interact with the contract

Included with the `pet-shop` Truffle Box was code for the app’s front-end. That code exists within the `src/` directory.

The front-end doesn’t use a build system (webpack, grunt, etc.) to be as easy as possible to get started. The structure of the app is already there; we’ll add in the functions unique to Ethereum.

1\. Open `/src/js/app.js` in a text editor.

2\. Examine the file. Note that there is a global `App` object to manage our application, load in the pet data in `init()` and then call the function `initWeb3()`. The [web3 JavaScript library](https://github.com/ethereum/web3.js/) interacts with the Ethereum blockchain. It can retrieve user accounts, send transactions, interact with smart contracts, and more.

3\. The current file has some _incomplete functions_ that you must fill in. Replace the old code and paste this **new code**:

```
App = {
  web3Provider: null,
  contracts: {},
  init: async function() {
    // Load pets.
    $.getJSON('../pets.json', function(data) {
      var petsRow = $('#petsRow');
      var petTemplate = $('#petTemplate');
      for (i = 0; i < data.length; i ++) {
        petTemplate.find('.panel-title').text(data[i].name);
        petTemplate.find('img').attr('src', data[i].picture);
        petTemplate.find('.pet-breed').text(data[i].breed);
        petTemplate.find('.pet-age').text(data[i].age);
        petTemplate.find('.pet-location').text(data[i].location);
        petTemplate.find('.btn-adopt').attr('data-id', data[i].id);
        petsRow.append(petTemplate.html());
      }
    });
    return await App.initWeb3();
  },  initWeb3: async function() {
    //----
    // Modern dapp browsers...
    if (window.ethereum) {
      App.web3Provider = window.ethereum;
      try {
        // Request account access
        await window.ethereum.enable();
      } catch (error) {
        // User denied account access...
        console.error("User denied account access")
      }
    }
    // Legacy dapp browsers...
    else if (window.web3) {
      App.web3Provider = window.web3.currentProvider;
    }
    // If no injected web3 instance is detected, fall back to Ganache
    else {
      App.web3Provider = new     Web3.providers.HttpProvider('http://localhost:7545');
    }
    web3 = new Web3(App.web3Provider);
    //----
    return App.initContract();
  },  initContract: function() {
    //----
    $.getJSON('Adoption.json', function(data) {
      // Get the necessary contract artifact file and instantiate it with truffle-contract
      var AdoptionArtifact = data;
      App.contracts.Adoption = TruffleContract(AdoptionArtifact);      // Set the provider for our contract
      App.contracts.Adoption.setProvider(App.web3Provider);      // Use our contract to retrieve and mark the adopted pets
      return App.markAdopted();
    });
    //----    return App.bindEvents();
  },  bindEvents: function() {
    $(document).on('click', '.btn-adopt', App.handleAdopt);
  },  markAdopted: function(adopters, account) {
    //----
    var adoptionInstance;
    App.contracts.Adoption.deployed().then(function(instance) {
      adoptionInstance = instance;      return adoptionInstance.getAdopters.call();
    }).then(function(adopters) {
      for (i = 0; i < adopters.length; i++) {
        if (adopters[i] !== '0x0000000000000000000000000000000000000000') {
          $('.panel-pet').eq(i).find('button').text('Success').attr('disabled', true);
        }
      }
    }).catch(function(err) {
      console.log(err.message);
    });
    //----
  },  handleAdopt: function(event) {
    event.preventDefault();    var petId = parseInt($(event.target).data('id'));    //----
    var adoptionInstance;    web3.eth.getAccounts(function(error, accounts) {
      if (error) {
        console.log(error);
      }      var account = accounts[0];      App.contracts.Adoption.deployed().then(function(instance) {
        adoptionInstance = instance;        // Execute adopt as a transaction by sending account
        return adoptionInstance.adopt(petId, {from: account});
      }).then(function(result) {
        return App.markAdopted();
      }).catch(function(err) {
        console.log(err.message);
      });
    });
    //---
  }
};$(function() {
  $(window).load(function() {
    App.init();
  });
});
```

Here is what these functions do:

`initWeb3()` Checks if we are using modern Dapp browsers or the more recent versions of [MetaMask](https://github.com/MetaMask).

`initContract()` Retrieves the artifact file for our smart contract. **Artifacts are information about our contract such as its deployed address and Application Binary Interface (ABI)**. **The ABI is a JavaScript object defining how to interact with the contract including its variables, functions and their parameters.** We then call the app's `markAdopted()` function in case any pets are already adopted from a previous visit.

`markAdopted()` After calling `getAdopters()`, we then loop through all of them, checking to see if an address is stored for each pet. Ethereum initializes the array with 16 empty addresses. This is why we check for an empty address string rather than null or other falsey value. Once a `petId` with a corresponding address is found, we disable its Adopt button and change the button text to "Success", so the user gets some feedback.

`handleAdopt()` We get the deployed contract and store the instance in `adoptionInstance`. We're going to send a **transaction** instead of a call by executing the `adopt()` function with both the pet's ID and an object containing the account address. Then, we proceed to call our `markAdopted()` function to sync the UI with our newly stored data.

