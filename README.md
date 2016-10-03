The code in `rep_distribution.js` can be loaded into a geth console to initialize the rep contract.

Note that at the top of this file the line `primaryAddress = eth.accounts[0];`

If you'd like to initiate transactions from a different account, please change this.

Copying this into the console takes a very long time due to the size of the balance/address arrays. Instead, it is best to launch get with `--preload rep_distribution.js console`

To load the rep contract, call
`loadRepContract()`
Once the contract is ready to be used you will see output in the console indicating the rep contract's address.

To initialize the contract with rep balances, call
`initializeRepBalances(0)`

To validate that the balances on the contract match the input, call
`validateBalances()`

If you'd like to validate your own balnce, you can do `repContract.balanceOf.call(address) / fxp`;


How to Load the Augur Contract Onto the Real Chain for the First Time


If you've never used geth install it.

Make an account geth account new if you don't already have one

Send 3 eth to it [takes about 1.8 but just to be safe]

git clone https://github.com/joeykrug/rep_distribution

geth --preload rep_distribution.js --unlock "address" console

By default, transactions will be initated by the account in eth.accounts[0]. If this is not the same as the account you unlocked when launching geth, do

`primaryAddress=your_address`

In the console, first load load the contract by calling:
`loadRepContract()`

Once the contract has been loaded, you will see its address printed to the console.

Initialize the contracts by calling
`initializeRepBalances(0)`

This will intialize the rep balances in batches of 100. Once this is complete, check to make sure everything looks good:

Calling `validateBalances()` will confirm that the contract's balances line up with the input arrays. Any discrepancies will be output to the console.

Call `repContract.getSeeded.call()` to confirm that the contract is marked as seeded (Should return 1).

Double check that the totalSupply is 11 million by doing `repContract.totalSupply.call() / fxp`


If you don't want to load your own contract and just want to validate someone else's, preload the same js into your console and do

`repContract = eth.contract(abi).at(contract_address);`
