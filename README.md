# Decentralized Autonomous Organizations in Blockchain and a practical demonstration on how they can influence direct-democracies.



An application of blockchain that is not talked about enough is concerning the implications it can have on direct-democracies. Unlike representative democracies, in which all the affected voters vote for a representative that makes the decisions for them, direct democracy skips the representative, and all participants, well, participate directly in the decision-making process.

Direct-democracies (and more specifically anarchist communities) historically had to face many challenges with regards to authority and physicality. A truly anonymous, horizontal online anarchist community is virtually never heard of because it’s impossible to achieve. With DAOs, organizations can be built horizontally, where there is no central figure to control every aspect of the organization and away from the influence of the governments. In the age of the internet, where communities can be spread worldwide, DAOs provide anonymity, transparency, equality, and automation efficiency away from the influence of governments and authorities.


One of the most important aspects of a successful DAO is voting on issues that impact all members of the organization, and Blockchain presents a natural progression to the voting process. 


## Technical Demonstration:

OpenZeppelin provides a library of smart contracts code that is community-vetted and has been thoroughly tested in production, making it an ideal starting point for any developer looking to get started with writing smart contracts. They provide battle-tested implementations of the ERC (Ethereum Request for Comment) standards.

This project is a simple DOA using OpenZeppelin Governor, which is provided specifically for DOA applications. Here is the scenario: 

Members of a DAO **(Token Holders)** called ‘Direct-Democracy’ want to build a gym. They need to create a proposal to vote **(Governance)** on that, if approved, will release predetermined funds from a communal bank **(Treasury)** to a builders cooperative **(Recipient)**. This money will be transferred after a time delay **(TimeLock)**.

First, let’s define the roles simply:
```
- Token Holders (Voters) → The people who will cast the votes on proposals.
- Treasury → A community bank where the budget is stored.
- Recipient → Once a vote is approved, the money will be released to this entity.
```
To achieve this, we will need 5 smart-contracts on the blockchain, let’s define them:
```
1. Token (ERC20Votes) → The cryptocurrency which the voters will own, and need to own to be members of the DAO and able to vote on proposals. In our example this token is called ‘FDC’.
2. Treasury → Where the funds are stored. The votes are to decide what to do with these funds.
3. Recipient → Where the funds will be sent to once a proposal has been approved. In our example, the builders cooperative.
4. Governance → Where proposals are created. In our example, there is an encoded function that will call on the treasury contract to release the funds.
5. TimeLock → A time delay imposed by the governance before firing the encoded function, if the proposal passes.
```

### Technology and stacks used:
- **Solidity**: To write the smart contracts.
- **Web3.js**: Interacting with the blockchain.
- **Truffle**: Developing Ethereum Framework.
- **Gnache**: This will give us 10  (local) ethereum blockchain addresses to simulate our token holders (Voters).


### Initial setup:
1. Install NodeJS.
2. Install Truffle. To check if you have it already, type `truffle version` in Terminal. If you don’t have it, you can install it with `npm i -g truffle`.
3. Install Ganache CLI with `npm install -g ganache-cli`. you can also use the [GUI version of Ganache](https://trufflesuite.com/ganache/) but I personally have had some errors with it on my machine.
4. Clone or Download the Repository.
5. Install Dependencies `npm install`.

### Explore the Project:
Under the ‘Contracts’ folder, you’ll see all the contracts we need for the project. Notice that in the ‘Token.sol’ file, the ERC20Votes contract is specifically imported from the OpenZeppelin library. The contract works similar to the regular ERC20, but was made for use-cases similar to ours. It has a mint function and a burn function, and a unique AfterTokenTransfer function that we need.

![ERC20Votes Smart Contract Screenshot](/assets/ERC20Votes.png?raw=true)



In ‘Migration/deploy-contracts.js’ is where we define the name `Direct Democracy` and symbol of our token `FDC`. We are also setting up our voters, in our case 5 which we will assign to the addresses Ganache will give us, and each address will get 50 ethers.

![Token Name and Symbol](/assets/DAO.png?raw=true)

```
Notice: min_Delay is set to 0, but this is just for testing purposes as we’re using ganache-cli.
```


Start Ganache by entering ‘ganache-cli' in a separate terminal. By default ganache starts @ port 8545, but you can change that to a port of your choice in the `truffle-config.js` file. If you change the port, you can start ganache using the following: “ganache-cli -p xxxx’.
![truffle-config.js screenshot ](/assets/port.png?raw=true)

![Ganachi-cli screenshot](/assets/ganache.png?raw=true)

As you can see here ganache gave 10 accounts each with 100 fake ETH, and their private keys. These keys are public so it goes without saying don’t send real money.

Now we’re getting to the action; deploy your contracts `truffle migrate --reset`.
If successfully deployed, you should see in the summary "Total Deployments: 5” and with that all our contracts have been deployed successfully.

![Contract Depolyment process screenshot](/assets/deployment.png?raw=true)

Now run the actual governance script and watch the whole thing come together `truffle exec ./scripts/1_create_proposal.js`

![Proposal Results screenshot](/assets/proposal.png?raw=true)
Examine the results we got and cross-reference with the functions in `1_create_proposal.js` file to see how each function plays a role in the proposal.

![Screenschot of 1_create_proposal.js file](/assets/create_proposal.png?raw=true)



And with that, we have successfully demonstrated a DAO voting mechanism that respects anonymity, is fully transparent and traceable, tamper-proof, and automated. 

Challenges remain concerning scalability with DAO and gas fees, but that goes for all blockchain implementations currently. Some startups have already structured as a DAO and there is no doubt that as scalability issues get solved, bigger communities and societies will slowly start adopting DAO and blockchain systems in general.




Credits:
- OpenZeppelin
- Gregory @ DappUniversity
- Patrick Collins
