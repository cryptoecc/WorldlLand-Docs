# What is WorldLand?

### **WorldLand: Expanding the Ethereum Ecosystem with a Bottom-Up Approach**

This white paper introduces WorldLand, an L2 or side chain of Ethereum, designed as a bottom-up solution to enhance the Ethereum ecosystem. Recognizing that the blockchain trilemma cannot be fully addressed by a single blockchain, WorldLand proposes the utilization of decentralized security blockchains, referred to as DeSecure blockchains, to achieve scalability while preserving decentralization and security. By connecting multiple side chains in parallel, WorldLand aims to increase block space and enhance transaction processing capabilities by integrating sub-national chains, local chains, and application chains.



WorldLand seeks to utilize the Proof-of-Work (PoW) consensus algorithm, which is not only simple and robust but also operates with independent peers that do not require constant information exchange. This characteristic reduces the network's influence on the consensus process. With PoW, each block records the number of independent nodes participating in consensus. Reversing a specific block would require securing more nodes than the number recorded in the block header. In other words, attempting to launch a reversible attack becomes costly, ensuring irreversibility.



However, traditional PoW systems have come under scrutiny due to their significant energy consumption, equivalent to that of a small country, for solving computational puzzles to elect block-creating nodes. WorldLand acknowledges this energy overconsumption problem associated with PoW and aims to provide a solution for it.



***

### Energy Efficient Green VCA (Verifiable Computation Algorithm) Matrix

WorldLand recognizes that Proof-of-Work (PoW) is the most secure consensus algorithm for implementing a robust network. However, the significant issue with PoW is its immense energy consumption. As of early 2022, annual energy consumption for PoW had reached 138 terawatt-hours, surpassing the electricity consumption of countries like Norway. This energy usage leads to annual CO2 emissions equivalent to that of Belgium, amounting to 114 million tonnes. To address this problem, WorldLand has developed a consensus algorithm that achieves energy efficiency through the implementation of a Verifiable Coin Toss Function and Error Correction Code.



While maintaining the strong security and decentralization of PoW, WorldLand incorporates technical measures to conserve energy. Instead of all nodes expending energy on puzzle-solving to elect a miner, the coin toss technique is applied. In this approach, when all nodes participate in the consensus process, they each toss a coin. Only a certain percentage of nodes (e.g., 10%) are self-elected and incentivized to participate in the consensus. By providing a means of verifying the evidence of self-election, honest participation is enforced. The randomly elected nodes then engage in ECCPoW (Error Correction Code Proof-of-Work) mining, resulting in a significant reduction in energy consumption. The election probabilities are automatically adjusted based on the overall network size. For instance, in the initial stages of a small network, the election probability may be set to 100%. As the network grows larger, it can be adjusted to approximately 5%. Through the Green VCA matrix, we aim to solve Post-Quantum security and environmental issues; while maintaining security, decentralization, and time energy assets at an appropriate level.



Green VCAs offer protection against double-spending attacks. The primary advantage of Green VCA consensus technology is that it does not require communication between nodes to reach consensus. Each node independently performs PoW operations to achieve consensus. Simply put, when a node discovers the solution to a puzzle problem, it publishes the answer. This lack of communication requirements allows a large number of nodes to participate in consensus. The system's simplicity enables reliable operation even with a multitude of participating nodes.



***

### Securing ASIC and Quantum Computer Resistance with Error Correction Code-based PoW

Existing Proof-of-Work (PoW) systems face challenges related to decentralization, particularly due to expensive Application-Specific Integrated Circuit (ASIC) devices. Additionally, the advent of quantum computers poses a significant threat to the decentralization of most cryptocurrency projects. Quantum computers have the potential to accelerate centralization by creating barriers for general users to participate in mining. To address these concerns, WorldLand implements measures to maintain decentralization while securing against ASIC devices using Error Correction Code-based PoW and protecting against quantum computer attacks using code theory.



By employing Error Correction Code-based PoW, WorldLand mitigates the influence of expensive ASIC devices on the network. The utilization of error correction codes helps ensure fair participation in the consensus process, preventing ASICs from dominating mining activities. This approach contributes to preserving decentralization and equal opportunities for miners, as ASICs are less effective compared to traditional PoW systems.



Furthermore, WorldLand incorporates code theory to enhance resistance against quantum computer attacks. Quantum computers have the potential to break traditional cryptographic algorithms, which could compromise the security of blockchain networks. By leveraging code theory, WorldLand strengthens the cryptographic mechanisms used within its system, making it more resilient against potential quantum threats. This helps safeguard the decentralization of the network and ensures the long-term security of WorldLand in the presence of advanced quantum computing technology.



***
