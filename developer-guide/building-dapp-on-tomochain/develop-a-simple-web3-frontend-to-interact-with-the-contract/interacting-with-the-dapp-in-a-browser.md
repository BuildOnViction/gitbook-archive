# Interacting with the Dapp in a browser

Now we’re ready to use our Dapp!

### 1. Install and configure MetaMask <a href="#4986" id="4986"></a>

1. Install the [MetaMask browser extension](https://metamask.io) in Chrome or FireFox.
2. Once installed, you’ll see the MetaMask fox icon next to your address bar. Click the icon and MetaMask will open up.
3. Create a New password. Then, write down the Secret Backup Phrase and accept the terms. By default, MetaMask will create a new Ethereum address for you.

![](https://miro.medium.com/max/60/1\*tV2bQfZ2vVhvpOOwKY0Y5g.png?q=20)![](https://miro.medium.com/max/1828/1\*tV2bQfZ2vVhvpOOwKY0Y5g.png)Initiating MetaMask

4\. Now we’re connected to the Ethereum network, with a brand new wallet with 0 ETH.

5\. Let’s now connect MetaMask to TomoChain (testnet). Click the menu with the “Main Ethereum Network” and select **Custom RPC**. Use the [Networks data from TomoChain](https://docs.tomochain.com/general/networks/) (testnet) and click **Save**

![](https://miro.medium.com/max/60/1\*Dm4qhGJOjnolRwxX-VN94w.png?q=20)![](https://miro.medium.com/max/1424/1\*Dm4qhGJOjnolRwxX-VN94w.png)Connecting MetaMask to TomoChain (testnet)

6\. The network name at the top will switch to say “TomoChain testnet”. Now that we are on TomoChain network we can import TomoChain wallets.

We could use the TOMO wallet we created previously, but better **let’s create a new TOMO wallet** and add a few TOMO tokens — _you know how to do it_.

7\. Once you have created your new TOMO wallet, **copy the private key**. Back to MetaMask, click on the top-right circle and select **Import Account.** Paste the private key and _voilà_! Your TOMO wallet is loaded in MetaMask

![](https://miro.medium.com/max/60/1\*AjEHidU-h0Ae0CXTsQUJ5Q.png?q=20)![](https://miro.medium.com/max/1298/1\*AjEHidU-h0Ae0CXTsQUJ5Q.png)Importing a wallet

### 2. Using the Dapp <a href="#9432" id="9432"></a>

We will now start a local web server and interact with the Dapp. We’re using the `lite-server`. This shipped with the `pet-shop` Truffle box.

The settings for this are in the files `bs-config.json` and `package.json`, if you want to take a look. These tell npm to run our local install of `lite-server` when we execute `npm run dev` from the console.

1. Start the local web server:

```
npm run dev
```

The dev server will launch and automatically open a new browser tab containing your Dapp.![](https://miro.medium.com/max/60/1\*gq766GpFC3UUCMoPW\_3Isw.png?q=20)![](https://miro.medium.com/max/2204/1\*gq766GpFC3UUCMoPW\_3Isw.png)Pete’s Pet Shop

Normally, a MetaMask notification automatically requests a connection.

2\. To use the Dapp, click the **Adopt** button on the pet of your choice.

3\. You’ll be automatically prompted to approve the transaction by MetaMask. Set some Gas and click **Confirm** to approve the transaction

![](https://miro.medium.com/max/60/1\*KNOJi0WwGoYF7jy\_AQz43Q.png?q=20)![](https://miro.medium.com/max/1378/1\*KNOJi0WwGoYF7jy\_AQz43Q.png)Adoption transaction review

4\. You’ll see the button next to the adopted pet change to say **“Success”** and become disabled, just as we specified, because the pet has now been adopted.

![](https://miro.medium.com/max/46/0\*iwMICrpZrGfJiNSY.png?q=20)![](https://miro.medium.com/max/988/0\*iwMICrpZrGfJiNSY.png)Adoption success

And in MetaMask you’ll see the transaction listed

![](https://miro.medium.com/max/44/1\*iqZsMFlAA3NCkOO-xfEjiQ.png?q=20)![](https://miro.medium.com/max/746/1\*iqZsMFlAA3NCkOO-xfEjiQ.png)MetaMask transaction

**Congratulations!** You have taken a huge step to becoming a full-fledged Dapp developer. You have all the tools you need to start making more advanced Dapps and now you can make your Dapp live for others to use deploying to TomoChain.
