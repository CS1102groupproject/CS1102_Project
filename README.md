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

<div/>

  <div id="bitcoinPage" class="page">
            <h2>Bitcoin Analysis</h2>
            <h3>Consensus Mechanism: Proof-of-Work (PoW)</h3>
            <p>Miners are required to find a random number that makes the hash have a leading number of zeros to finish the crypto-puzzle. The complexity of the puzzle is adjusted every 2 weeks to maintain the block time around 10 minutes (Nakamoto, n.d.). Hence, Bitcoin applies PoW to ensure that no individual can control the network.</p>
            
            <h3>Transaction Speed and Scalability</h3>
            <p>Transactions are grouped into blocks added every ~10 minutes. Merkle Trees compress transactions into a single root hash to save storage. However, Bitcoin processes only approximately 7 transactions per second, which is relatively slow (How Bitcoin Can Scale | River Learn - Bitcoin Basics, n.d.).</p>
            
            <h3>Privacy and Anonymity</h3>
            <p>When executing a transaction, users employ different random-looking (i.e., one-time) pseudonymous public keys (i.e., addresses) to protect their privacy. Privacy is protected due to the randomness as long as the addresses remain unlinked to the user’s identity (Buczak, 2024).</p>
            
            <h3>Smart Contracts and Programmability</h3>
            <p>Only simple scripting rules are applied, such as unlocking transactions based on the specific date (Script - Bitcoin Wiki, n.d.). The complexity of the logic is not as high as in other cryptocurrencies, hence, building complex applications like NFTs is not feasible.</p>
            
            <h3>Energy Efficiency</h3>
            <p>Since PoW is used, it requires consuming massive amounts of electricity for mining (Cambridge Blockchain Network Sustainability Index: CBECI, n.d.). Although energy consumption is high, security is ensured. This issue might be mitigated by using renewable energy.</p>
        </div>

        <div id="ethereumPage" class="page">
            <h2>Ethereum Analysis</h2>
            <h3>Consensus Mechanism: Proof-of-Stake (PoS)</h3>
            <p>PoS is a mechanism used by Ethereum to validate transactions and create new blocks without relying on PoW. Validators are chosen to propose and attest to new blocks via a random selection algorithm, weighted by the amount of ETH staked and time since the last selection (Proof-of-stake (POS), n.d.). Other validators verify the blocks and vote. A block becomes irreversible once confirmed.</p>
            
            <h3>Transaction Speed and Scalability</h3>
            <p>ETH uses sharding and rollups to increase transaction speed. Data Sharding divides Ethereum’s blockchain into smaller parallel shards. Rollups process transactions off-chain, bundle them, compress the data onto Ethereum, and provide validity proofs for verification. Ethereum’s transaction speed targets to reach around 100,000 transactions per second, but currently the TPS stays at 173.6 (Sergeenkov, 2024).</p>
            
            <h3>Privacy and Anonymity</h3>
            <p>ETH uses zk-SNARKs, Tornado Cash, and Stealth Addresses to provide a trustworthy system (Brown, 2024). Zk-SNARKs and Tornado Cash can be used together to hide transaction details. Zk-SNARKs generates a new encrypted address to prove ownership without leaking personal information, while Tornado Cash acts as a decentralized mixer to enhance privacy.</p>
            
            <h3>Smart Contracts and Programmability</h3>
            <p>ETH utilizes Turing-complete smart contracts, which are compiled into EVM bytecode and auto-execute when conditions are met (Team, 2024). These contracts run on the Ethereum Virtual Machine (EVM). The EVM supports loops, conditional logic, and complex computations, making its programmability highly flexible.</p>
            
            <h3>Energy Efficiency</h3>
            <p>Due to the adoption of PoS, validators secure the network by staking ETH, not by solving complex crypto-puzzles, reducing energy consumption by 99.95% (How Does Ethereum Work? An Introduction to ETH, n.d.). However, some argue that staking centralizes power among those with more ETH.</p>
        </div>

        <div id="usdtPage" class="page">
            <h2>USDT Analysis</h2>
            <h3>Consensus Mechanism: Depends on the host chain</h3>
            <p>USDT itself is not a standalone blockchain; its consensus mechanism depends on the host chain. For example, ERC-20 USDT uses PoS, TRC-20 USDT uses DPoS, and the original USDT uses PoW. Thus, security varies.</p>
            
            <h3>Transaction Speed and Scalability</h3>
            <p>Since USDT’s consensus mechanism relies on the host chain, transaction speed and scalability vary. For instance, it is slower on ERC-20 USDT (173.6 TPS) than on SPL-based chains (65,000 TPS) (Ledger, 2025).</p>
            
            <h3>Privacy and Anonymity</h3>
            <p>USDT records transactions on transparent ledgers, allowing anyone to trace them. While different blockchains offer varying privacy systems (e.g., pseudonymous addresses, mixers, decentralized exchanges), USDT’s privacy remains very low due to traceability.</p>
            
            <h3>Smart Contracts and Programmability</h3>
            <p>USDT itself is not programmable and is compatible with the host chain’s apps. It lacks built-in smart contracts. However, it follows the host blockchain’s smart contract rules. Despite not being programmable, USDT is often integrated into programmable ecosystems.</p>
            
            <h3>Energy Efficiency</h3>
            <p>Since USDT’s consensus mechanism relies on the host chain, energy efficiency varies by blockchain. For example, it consumes less energy on PoS chains (e.g., ERC-20) and more on PoW chains (e.g., Bitcoin/original USDT). Its eco-friendliness depends on the underlying blockchain.</p>
        </div>

        <div id="tablePage" class="page">
            <h2>Cryptocurrency Comparison</h2>
            <div class="table-filters">
                <button class="filter-btn" onclick="toggleFeatureHighlight('Consensus Mechanism')">Consensus Mechanism</button>
                <button class="filter-btn" onclick="toggleFeatureHighlight('Transaction Speed')">Transaction Speed</button>
                <button class="filter-btn" onclick="toggleFeatureHighlight('Privacy & Anonymity')">Privacy & Anonymity</button>
                <button class="filter-btn" onclick="toggleFeatureHighlight('Smart Contracts')">Smart Contracts</button>
                <button class="filter-btn" onclick="toggleFeatureHighlight('Energy Efficiency')">Energy Efficiency</button>
            </div>
            <div class="comparison-table-container">
                <table class="comparison-table" id="comparisonTable">
                    <tr>
                        <th>Feature</th>
                        <th>Bitcoin (BTC)</th>
                        <th>Ethereum (ETH)</th>
                        <th>USDT</th>
                    </tr>
                    <tr>
                        <td>Consensus Mechanism</td>
                        <td>Proof of Work (PoW)<br>- Adjusted every 2 weeks<br>- 10-minute block target</td>
                        <td>Proof of Stake (PoS)<br>- Validators stake ETH<br>- Finality after confirmation</td>
                        <td>Host chain dependent<br>- ERC-20 (PoS)<br>- TRC-20 (DPoS)</td>
                    </tr>
                    <tr>
                        <td>Transaction Speed</td>
                        <td>~7 TPS<br>- 10-minute blocks<br>- Layer 2 (Lightning Network) solutions</td>
                        <td>173.6 TPS base<br>- 100k+ TPS target<br>- Sharding + rollups</td>
                        <td>Chain-dependent<br>- ERC-20: 173.6 TPS<br>- SPL: 65,000 TPS</td>
                    </tr>
                    <tr>
                        <td>Privacy & Anonymity</td>
                        <td>Pseudonymous addresses<br>- One-time public keys<br>- No KYC</td>
                        <td>Enhanced privacy<br>- zk-SNARKs<br>- Tornado Cash mixer</td>
                        <td>Fully traceable<br>- Transparent ledger<br>- Centralized oversight</td>
                    </tr>
                    <tr>
                        <td>Smart Contracts</td>
                        <td>Basic scripting<br>- Time-locked transactions<br>- No complex logic</td>
                        <td>Turing-complete<br>- EVM execution<br>- Complex dApps/NFTs</td>
                        <td>No native support<br>- Relies on host chain<br>(e.g., Ethereum/Solana)</td>
                    </tr>
                    <tr>
                        <td>Energy Efficiency</td>
                        <td>High consumption<br>- PoW mining<br>- Renewable solutions proposed</td>
                        <td>99.95% reduction<br>- Post-Merge PoS<br>- ~0.0026 TWh/yr</td>
                        <td>Host chain dependent<br>- Efficient on PoS<br>- Inefficient on PoW</td>
                    </tr>
                </table>
            </div>
        </div>

        <div id="referencePage" class="page">
            <h2>References</h2>
            <ol class="reference-list">
                <li>Nakamoto, S. (n.d.). Bitcoin: A Peer-to-Peer Electronic Cash System. <a href="https://bitcoin.org/bitcoin.pdf" target="_blank">https://bitcoin.org/bitcoin.pdf</a></li>
                <li>How Bitcoin can scale | River Learn - Bitcoin Basics. (n.d.). River. <a href="https://river.com/learn/how-bitcoin-can-scale/" target="_blank">https://river.com/learn/how-bitcoin-can-scale/</a></li>
                <li>Buczak, A. (2024, December 30). Is Bitcoin anonymous? The myth of anonymity debunked. ULAM LABS. <a href="https://www.ulam.io/blog/is-cryptocurrency-anonymous#" target="_blank">https://www.ulam.io/blog/is-cryptocurrency-anonymous#</a></li>
                <li>Script - Bitcoin Wiki. (n.d.). <a href="https://en.bitcoin.it/wiki/Script" target="_blank">https://en.bitcoin.it/wiki/Script</a></li>
                <li>Cambridge Blockchain Network Sustainability Index: CBECI. (n.d.). <a href="https://ccaf.io/cbnsi/cbeci" target="_blank">https://ccaf.io/cbnsi/cbeci</a></li>
                <li>Proof-of-stake (POS). (n.d.). ethereum.org. <a href="https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/" target="_blank">https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/</a></li>
                <li>Sergeenkov, A. (2024, October 17). Ethereum’s surge roadmap targets 100,000+ transactions per second. Forbes. <a href="https://www.forbes.com/sites/digital-assets/2024/10/17/ethereums-surge-roadmap-targets-100000-transactions-per-second/" target="_blank">https://www.forbes.com/sites/digital-assets/2024/10/17/ethereums-surge-roadmap-targets-100000-transactions-per-second/</a></li>
                <li>Brown, S. (2024, December 9). Privacy in Ethereum — Stealth addresses - Simon Brown - medium. Medium. <a href="https://simbro.medium.com/privacy-in-ethereum-stealth-addresses-f05016109010" target="_blank">https://simbro.medium.com/privacy-in-ethereum-stealth-addresses-f05016109010</a></li>
                <li>Team, L. (2024, November 21). How EVM compiles smart contracts: A detailed explanation. LCX. <a href="https://www.lcx.com/how-evm-compiles-smart-contracts-explained/" target="_blank">https://www.lcx.com/how-evm-compiles-smart-contracts-explained/</a></li>
                <li>How does Ethereum work? An introduction to ETH. (n.d.). <a href="https://crypto.com/en/university/how-does-ethereum-work-introduction-to-eth" target="_blank">https://crypto.com/en/university/how-does-ethereum-work-introduction-to-eth</a></li>
                <li>Ledger. (2025, February 6). Everything you need to know about the SPL Ecosystem | Ledger. <a href="https://www.ledger.com/academy/topics/blockchain/everything-you-need-to-know-about-the-spl-ecosystem" target="_blank">https://www.ledger.com/academy/topics/blockchain/everything-you-need-to-know-about-the-spl-ecosystem</a></li>
            </ol>
        </div>
    </main>

    <footer>
        <p>Learn more about our Team</p>
    </footer>

<script>
        document.getElementById('comparisonButton').addEventListener('click', function(e) {
            e.stopPropagation();
            const dropdown = document.getElementById('comparisonDropdown');
            dropdown.style.display = dropdown.style.display === 'block' ? 'none' : 'block';
        });

        document.addEventListener('click', function(e) {
            if (!e.target.closest('.dropdown')) {
                document.getElementById('comparisonDropdown').style.display = 'none';
            }
        });

        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(page => {
                page.style.display = 'none';
            });
            document.getElementById(pageId).style.display = 'block';
        }

        document.getElementById('homeButton').addEventListener('click', () => {
            showPage('homePage');
        });

        document.getElementById('clickMe').addEventListener('click', function() {
            const infoDiv = document.getElementById('Showmore');
            infoDiv.style.display = infoDiv.style.display === 'none' ? 'block' : 'none';
        });

        function toggleFeatureHighlight(feature) {
            const buttons = document.querySelectorAll('.filter-btn');
            const table = document.getElementById('comparisonTable');
            const allRows = Array.from(table.querySelectorAll('tr:not(:first-child)'));
            const activeRow = allRows.find(row => 
                row.querySelector('td:first-child').textContent.trim() === feature
            );

            buttons.forEach(btn => btn.classList.remove('active'));
            const currentBtn = Array.from(buttons).find(b => b.textContent.trim() === feature);
            const wasActive = currentBtn.classList.contains('active');
            
            if (!wasActive) {
                currentBtn.classList.add('active');
                table.classList.add('hide-features');
                allRows.forEach(row => {
                    row.style.display = row === activeRow ? '' : 'none';
                });
            } else {
                table.classList.remove('hide-features');
                allRows.forEach(row => row.style.display = '');
            }
        }

        showPage('homePage');
    </script>
</body>
</html>

