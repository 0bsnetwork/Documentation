# Node

0bsnetwork is a peer-to-peer, truly decentralized blockchain network running NG-DPoS consensus algorithm. That means that the processing of data and transactions is not done in a central location or one \(set of\) server\(s\). Instead, processing of data and transactions is done by a network of equal peers, each of which does exactly the same job and has the same "rights" on the network. We as the founders of the platform have equal power over the network as any other \(independent\) operator of a node. 

Nodes on the 0bsnetwork serve four critical roles:

1. Receive and verify the validity of all \(token and data\) transactions sent by the end-users/accounts, forging them into blocks and/or confirming that blocks forged by other nodes are indeed correct and valid.
2. Propagate all the information \(data and events\) to their peers \(other nodes on the network\) as quickly and efficiently as possible.
3. Answer queries for end users about the state of the blockchain, all assets/tokens and accounts
4. Execute smart contract code and implement rules integrated into smart accounts

The job of a node is to store the blockchain data, pass along the data to other nodes, and ensure newly added blocks are valid. Validation entails ensuring that the format of the block is correct, all hashes in the new block were computed correctly, the new block contains the hash of the previous block \(thus forming an immutable blockchain\), and each transaction in the block is valid and signed by the appropriate party\(ies\). Nodes may, but don't have to, also act as mining/forging nodes \(i.e., generating new blocks\), The forging node checks that each transaction is valid before including it into a block, since the other nodes would reject the block if it included invalid transactions.

End user software can connect to any node on the network and send their transactions to it, without experiencing any degradation in performance, provided that the node has sufficient resources and a stable internet connection. Any node may propose new transactions, and these proposed transactions are propagated between nodes until they are eventually added to a block.

