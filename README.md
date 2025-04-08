<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CS1102 Blockchain Analysis</title>
    <style>
        body {
            font-family: 'Times', serif;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            background-color: #f7f7f7;
            color: #333;
            overflow-x: hidden;
        }
        header {
            position: relative;
            background: #6a89cc;
            color: white;
            padding: 2rem;
            text-align: center;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        .header-buttons {
            position: absolute;
            top: 20px;
            right: 20px;
            display: flex;
            gap: 10px;
        }
        .header-button {
            background: transparent;
            border: 2px solid white;
            color: white;
            padding: 0.5rem 1.5rem;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1rem;
            transition: all 0.3s ease;
            font-family: 'Times', serif;
            position: relative;
        }
        .header-button:hover {
            background: white;
            color: #6a89cc;
        }
        .dropdown-content {
            display: none;
            position: absolute;
            top: 100%;
            left: 0;
            background-color: white;
            min-width: 160px;
            box-shadow: 0 8px 16px rgba(0,0,0,0.2);
            border-radius: 8px;
            overflow: hidden;
            z-index: 1;
        }
        .dropdown-content button {
            width: 100%;
            padding: 12px 16px;
            text-align: center;
            border: none;
            background: white;
            color: #333;
            border-bottom: 1px solid #eee;
            cursor: pointer;
            transition: all 0.2s ease;
            font-family: 'Times', serif;
        }
        .dropdown-content hr {
            margin: 0;
            border: 0;
            border-top: 1px solid #eee;
        }
        .dropdown-content button:hover {
            background: #6a89cc;
            color: white;
        }
        main {
            flex: 1;
            padding: 2rem;
            background: white;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.05);
            width: 100%;
            box-sizing: border-box;
        }
        .page {
            display: none;
            width: 100%;
            max-width: 100%;
            margin: 0 auto;
            padding: 0 2rem;
            box-sizing: border-box;
            word-wrap: break-word;
        }
        .active-page {
            display: block;
        }
        h2 {
            color: #34495e;
            margin-bottom: 1rem;
        }
        h3 {
            color: #2c3e50;
            margin: 1.5rem 0 0.5rem;
        }
        p {
            line-height: 1.6;
            margin-bottom: 1.5rem;
            overflow-wrap: break-word;
            max-width: 100%;
        }
        button {
            background-color: #6a89cc;
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
            background-color: #5a7fba;
        }
        footer {
            background: #34495e;
            color: white;
            text-align: center;
            padding: 1rem;
            width: 100%;
        }
        #Showmore {
            display: none;
            margin-top: 1rem;
            padding: 1rem;
            background: #e0f7fa;
            border-radius: 5px;
        }
        .comparison-table-container {
            overflow-x: auto;
            margin: 2rem 0;
            max-width: 100%;
        }
        .comparison-table {
            width: 100%;
            min-width: 800px;
            border-collapse: collapse;
        }
        .comparison-table th,
        .comparison-table td {
            padding: 1.2rem;
            border: 1px solid #ddd;
            text-align: left;
            vertical-align: top;
            word-break: break-word;
            min-width: 200px;
            max-width: 400px;
        }
        .comparison-table th {
            background-color: #6a89cc;
            color: white;
            position: sticky;
            top: 0;
            z-index: 3;
        }
        /* Make both the first header cell and first data cells sticky */
        .comparison-table th:first-child,
        .comparison-table td:first-child {
            position: sticky;
            left: 0;
            z-index: 2;
        }
        .comparison-table th:first-child {
            z-index: 4; /* Higher than other sticky elements */
        }
        .comparison-table tr:nth-child(even) td:first-child {
            background-color: #f8f9fa;
        }
        .comparison-table tr:nth-child(even) {
            background-color: #f8f9fa;
        }
        .table-filters {
            margin: 1rem 0;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 0.5rem;
        }
        .filter-btn {
            background: #6a89cc;
            color: white;
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
            text-align: center;
            white-space: nowrap;
        }
        .filter-btn.active {
            background: #34495e;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
        }
        .comparison-table.hide-features th:first-child,
        .comparison-table.hide-features td:first-child {
            display: none;
        }
        @media (max-width: 768px) {
            .comparison-table {
                font-size: 0.9rem;
            }
            .comparison-table th,
            .comparison-table td {
                padding: 0.8rem;
                min-width: 160px;
            }
            .filter-btn {
                padding: 0.5rem;
                font-size: 0.9rem;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="header-buttons">
            <button class="header-button" id="homeButton">Home</button>
            <div class="dropdown">
                <button class="header-button" id="comparisonButton">Comparison ▼</button>
                <div class="dropdown-content" id="comparisonDropdown">
                    <button onclick="showPage('bitcoinPage')">Bitcoin</button>
                    <button onclick="showPage('ethereumPage')">Ethereum</button>
                    <button onclick="showPage('usdtPage')">USDT</button>
                    <hr>
                    <button onclick="showPage('tablePage')">Table Comparison</button>
                </div>
            </div>
            <button class="header-button" id="referenceButton" onclick="showPage('referencePage')">References</button>
        </div>
        <h1>CS1102_The Mechanism and Applications of Blockchain</h1>
        <h2>Project Members:</h2>
        <p>Yeung Ho Fung 57847209<br>Law Ho Tat 57317481<br>Ma Chun Chiu 57134824<br>Chiu Tsz Ki 56615622</p>
    </header>


    <main>
        <div id="homePage" class="page active-page">
            <h2>About This Page</h2>
            <p>This page would like to show how blockchain works, the transactions of cryptocurrencies, especially the implementation of Bitcoin. A comparison of different cryptocurrency techniques will also be covered. Let's explore more about Blockchain together with us!</p>
            <button id="clickMe">Show More</button>
        <div id="Showmore">
            <h3>What are Blocks?</h3>
            <p>Blocks are a continuously growing list of ordered records. These blocks “are linked using cryptography. Each block contains a cryptographic hash of the previous block, a timestamp, and transaction data.</p>
            <h3>What is Blockchain?</h3>
            <p>Blockchain is a public, digital ledger which tracks real-time movements and transactions of assets. Each transaction is a single “block”, and each block links together to form a “chain” known as a “blockchain”. Encrypted data in the blocks are linked with one another permanently. A blockchain is a decentralized database that keeps a continuously growing list of ordered records called blocks. It records transactions of multiple computers, which record cannot be altered retroactively without modifying all corresponding subsequent blocks and networks. Each transaction is visible to participants within the network. It creates the audit history of each transaction and keeps records and reviews. When new data is added to the network, it is required to verify the legitimacy of the data according to the economic incentives or authority of the majority of nodes. This process is named the consensus mechanism. Cryptographic techniques secure the data in the blockchain, which makes it complicated to tamper with. Once the consensus is obtained, a new block will be created along the chain. All nodes will thereby be updated.
</p>
            <h3>How Blockchain Works?</h3>
            <p>Blockchain begins with the data exchanged between two parties in the form of money, deeds, contracts, customer details, medical records, or any other asset in digital form. Verification is required. The duration of the step taken will depend on the network’s parameters, which will be undertaken instantly or transcribed into secured records and pending transactions in the queue. The computers or servers in the network will then determine the transaction's validity according to the network rules.
</p>
           
            <p>A block contains a header referencing the previous block’s hash and the transactions. A hash contains 8 bytes using the algorithm agreed upon by the network. The linked hash provides security and interdependency of the chain. Before adding to form the block in the blockchain, it must be first validated. One of the methods is through proof consensus mechanisms (Proof of Work / Proof of Stake), solving the mathematical puzzle from the block’s header. Miners make extra changes to a variable to solve the blocks until it satisfies the requirements of the entire network; this is named “proof of work”. If someone maliciously attempts to manipulate the block and submit to the chain, the hash function will change to defence. The other nodes will then reject the block from entering the major chain in order to prevent corruption.
</p>
               
            <p>When the block is verified, the block is distributed to the entire network. The miner will be rewarded. Each node adds the corresponding node to the majority chain.</p>


</main>
</body>
</html>

