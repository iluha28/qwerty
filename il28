const ethers = require("ethers");
const {parseUnits, parseEther, Contract} = require('ethers');
const url = ""; // blockchain node
const privateKey = ""; // private key
const provider = new ethers.JsonRpcProvider(url);
const wallet = new ethers.Wallet(privateKey, provider);
const ERC20 = ""; // token address
const abi = [
  "function transfer(address to, uint amount)", 
  "function balanceOf(address) public view returns (uint)"
];

async function getBalance() {
  const balance = await provider.getBalance(wallet.address);
  const balanceInEth = ethers.formatEther(balance); // wei to ether
  console.log(balance.toString() / 1e18);
}

async function getERC20() {
  const contract = new Contract(ERC20, abi, provider);
  const balance = await contract.balanceOf(wallet.address);
  console.log(balance.toString() / 1e18);
}

async function sendEth(whomTransfer, numOfTokens) {
  const tx = await wallet.sendTransaction({
    to: whomTransfer, // to whom to transfer
    value: parseEther(numOfTokens) // number of tokens
  });

  console.log(tx.hash);
  const receipt = await tx.wait();
  console.log(receipt);
}

async function sendERC20(whomTransfer, numOfTokens) {
  const contract = new Contract(ERC20, abi, wallet);
  const amount = parseUnits(numOfTokens, 18); // number of tokens
  const tx = await contract.transfer(whomTransfer, amount); // to whom to transfer

  console.log(tx.hash);
  const receipt = await tx.wait();
  console.log(receipt);
} 

// getBalance()
// getERC20()
// sendEth("", "") // first param - wallet address, second - number of tokens
// sendERC20("", "")
