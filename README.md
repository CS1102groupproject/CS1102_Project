<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CS1102_The Mechanism and Applications of Blockchain</title>
    <style>
        body {
            font-family: 'Times', serif;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            background-color: #f7f7f7; /* Soft background */
            color: #333;
        }
        header {
            background: #6a89cc; /* Soft blue */
            color: white;
            padding: 2rem;
            text-align: center;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        main {
            flex: 1;
            padding: 2rem;
            max-width: 800px;
            margin: auto;
            background: white;
            border-radius: 8px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.05);
        }
        h2 {
            color: #34495e; /* Darker grayish-blue */
            margin-bottom: 1rem;
            font: Times;
        }
        p {
            line-height: 1.6;
            margin-bottom: 1.5rem;
        }
        button {
            background-color: #6a89cc; /* Soft blue */
            color: white;
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1rem;
            transition: background-color 0.3s;
            font-family: 'Times', serif;
            text-transform: uppercase;
        }
        button:hover {
            background-color: #5a7fba; /* Slightly darker blue */
        }
        footer {
            background: #34495e; /* Darker grayish-blue */
            color: white;
            text-align: center;
            padding: 1rem;
            position: relative;
            bottom: 0;
            width: 100%;
        }
        #Showmore {
            display: none; /* Initially hidden */
            margin-top: 1rem;
            padding: 1rem;
            background: #e0f7fa; /* Light cyan background */
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <header>
        <h1>CS1102_The Mechanism and Applications of Blockchain</h1>
        <h2>Project Members:</h2>
        <p>Yeung Ho Fung 57847209<br>Law Ho Tat 57317481<br>Ma Chun Chiu 57134824<br>Chiu Tsz Ki 56615622</p>
    </header>
    <main>
        <h2>About This Page</h2>
        <p>This page would like to show how blockchain works and the transactions of cryptocurrencies, especially the implementation of Bitcoin. A comparison of different cryptocurrency techniques will also be covered. Let's explore more about Blockchain together with us!</p>
        <button id="clickMe">Show More</button>
        <div id="Showmore">
            <h3>What are Blocks?</h3>
            <p>Blocks are a continuously growing list of ordered records. These blocks “are linked using cryptography. Each block contains a cryptographic hash of the previous block, a timestamp, and transaction data.</p>
            <h3>What is Blockchain?</h3>
            <p>Blockchain is a public, digital ledger which tracks real-time movements and transactions of assets. Each transaction is a                    single “block”, and each block links together to form a “chain” known as a “blockchain”. Encrypted data in the blocks are                    linked with one another permanently. A blockchain is a decentralized database that keeps a continuously growing list of                      ordered records called blocks. It records transactions of multiple computers, which record cannot be altered retroactively                   without modifying all corresponding subsequent blocks and networks. Each transaction is visible to participants within the                   network. It creates the audit history of each transaction and keeps records and reviews. When new data is added to the                       network, it is required to verify the legitimacy of the data according to the economic incentives or authority of the                        majority of nodes. This process is named the consensus mechanism. Cryptographic techniques secure the data in the blockchain,                which makes it complicated to tamper with. Once the consensus is obtained, a new block will be created along the chain. All                  nodes will thereby be updated.</p>
            <h3>How Blockchain Works?</h3>
            <p>Blockchain begins with the data exchanged between two parties in the form of money, deeds, contracts, customer details,                     medical records, or any other asset in digital form. Verification is required. The duration of the step taken will depend on                 the network’s parameters, which will be undertaken instantly or transcribed into secured records and pending transactions in                 the queue. The computers or servers in the network will then determine the transaction's validity according to the network                   rules.</p>
           
            <p>A block contains a header referencing the previous block’s hash and the transactions. A hash contains 8 bytes using the                     algorithm agreed upon by the network. The linked hash provides security and interdependency of the chain. Before adding to                   form the block in the blockchain, it must be first validated. One of the methods is through proof consensus mechanisms                       (Proof of Work / Proof of Stake), solving the mathematical puzzle from the block’s header. Miners make extra changes to a                    variable to solve the blocks until it satisfies the requirements of the entire network; this is named “proof of work”. If                    someone maliciously attempts to manipulate the block and submit to the chain, the hash function will change to defence. The                  other nodes will then reject the block from entering the major chain in order to prevent corruption. 
               
            <p>When the block is verified, the block is distributed to the entire network. The miner will be rewarded. Each node adds the                 corresponding node to the majority chain</p>
        </div>
    </main>
    <footer>
        <p>Learn more about our Team</p>
    </footer>
    <script>
        document.getElementById('clickMe').addEventListener('click', function() {
            const infoDiv = document.getElementById('Showmore');
            infoDiv.style.display = infoDiv.style.display === 'none' ? 'block' : 'none';
        });
    </script>
</body>
</html>
