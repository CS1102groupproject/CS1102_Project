<!DOCTYPE html>
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
        <p>This page would like to show how blockchain works, the transactions of cryptocurrencies, especially the implementation of Bitcoin. A comparison of different cryptocurrency techniques will also be covered. Let's explore more about Blockchain together with us!</p>
        <button id="clickMe">Show More</button>
        <div id="Showmore">
            <h3>What are Blocks?</h3>
            <p>Blocks are a continuously growing list of ordered records. These blocks are linked using cryptography. Each block contains a cryptographic hash of the previous block, a timestamp, and transaction data.</p>
            <h3>What is Blockchain?</h3>
            <p>A blockchain is a distributed database that maintains a continuously growing list of ordered records, called blocks. A blockchain is a decentralized, distributed, and public digital ledger used to record transactions across many computers so that the record cannot be altered retroactively without the alteration of all subsequent blocks and the consensus of the network.</p>
            <h3>How Blockchain Works?</h3>
            <p>Similar to databases and spreadsheets, Blockchain is a database where information is entered and stored. A blockchain is about how the data is structured and accessed.</p>
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
