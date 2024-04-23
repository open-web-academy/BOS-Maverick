# BOS + Maverick

This repository is an example of how to implement Maverick LP contracts in BOS to add liquidity to a pool in both left and right modes.

<img src="https://drive.google.com/uc?id=1NcAQb5QimcquiI3DCc2OZhdy3sIwHIAA" width="35%">

## How to implement the LP contract of Maverick in BOS?

To implement the Token Factory contract and be able to create new tokens from our BOS component we will have to make some configurations and calls to the contract methods.

The first thing we must do is to initialize our contract and call the corresponding ABI to obtain the information of the methods of the contract, for them we make use of the following lines:

```jsx
const factoryContract = "0xAc9221060455f60dfFF8bf8C4f601E500AC095D7";

const factoryAbi = fetch(
  "https://raw.githubusercontent.com/open-web-academy/BOS-TokenFactory/main/TokenFactoryABI.txt"
);
```

Once this is done, we will proceed to initialize each of the state variables as well as each of the methods to change their values.

```jsx
const [sender, setSender] = useState(null);
const [tokens, setTokens] = useState([]);
const [tokenName, setTokenName] = useState("MYTOKEN");
const [tokenSymbol, setTokenSymbol] = useState("MTKN");
const [initialSupply, setInitialSupply] = useState(10000);
const [minting, setMinting] = useState(false);
const [tabSelected, setTabSelected] = useState("factory");
```

As mentioned before, the Token Factory contract has two main methods, to call them from BOS we will have to do the following: 

**getTokens**: With this method we get each of the tokens created in the factory to later show them in the UI:

```jsx
const getTokens = () => {
  const factory = new ethers.Contract(
    factoryContract,
    factoryAbi.body,
    Ethers.provider().getSigner()
  );

  factory.getAllTokens().then((res) => {
    setTokens(res);
    console.log(res);
  });
};
```

**createToken**: With this method we create a new token, the parameters to be sent are the following:
  * **tokenName**: token name to create.
  * **tokenSymbol**: token symbol to craete.
  * **amount**: initial token supply to create.

```jsx

```

## How to test the Component?

To run this project in BOS you must run the widget (BOS-TokenFactory.jsx) on an available BOS gateway, for example: [near.social ](https://near.social/edit)

Once the code for the widget has been added we can render it by clicking on the preview button to render the component.

<img src="https://drive.google.com/uc?id=1oiuRLjC2RJDts2K57av4I5YzuGtSukVT" width="50%">

For this example you will also need to have installed and configured [metamask](https://metamask.io/) and [Sepolia](https://sepolia.dev/) network.

Once this is done, you can click **Connect Wallet** to run metamask and connect the component to your account.

<img src="https://drive.google.com/uc?id=1b9qgOoFL9a1eTi67aWYqH1UeGnYLa7Ye" width="50%">

Once metamask is connected we will be able to start interacting with the UI.

The first step to create a new token is to fill in the form with the three fields: token name, token symbol and token supply.

Then we must click on the "Create Token" button which will launch a transaction in metamask and we must confirm it to start with the creation of our token.

Finally we can go to the "Token List" tab where we can see all the tokens created with their respective addresses to add the token to metamask.

<img src="https://drive.google.com/uc?id=1S3nu7eEUs-7PW0kOT4VJpNZHdI5QaodR" width="50%">

## BOS Widget

Maverick: https://near.social/owa-is-bos.near/widget/BOS-Maverick
