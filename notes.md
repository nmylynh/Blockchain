# Blockchains

>A blockchain is, in the simplest of terms, a time-stamped series of immutable records of data that is managed by a cluster of computers not owned by any single entity. Each of these blocks of data (i.e. block) is secured and bound to each other using cryptographic principles (i.e. chain).

## Decentralization vs Centralization

![Decentralization](https://i.imgur.com/dXvOGTZ.pngs)

The blockchain network has **no central authority** — it is the very definition of a democratized system. Since it is a shared and immutable ledger, the information in it is open for anyone and everyone to see. Hence, anything that is built on the blockchain is by its very nature transparent and everyone involved is accountable for their actions.

On the other hand, **banks are a centralized system**. You trust the bank, so you give them your money and they look after it, charging you fees in exchange. But what if computer code had been written that could handle all of that stuff? What if nobody needs to make transfers or back up balances? The only people who needed to be involved with your money was you. And anyone you're transacting with. No need for a bank to check the validity of your transactions, no extra fees for sending money overseas; nothing. It's all in the code. You take the bank out of the middle, and use the computer code as a means of connecting you directly with other people. The balances and the transactions are held by everyone, that way the code can quickly check what is and isn't valid. Once it does, it check everyone else's copy of the balances and transactions, to make sure neither of you have cheated anything.

## Blockchain Structure

**A blockchain is a method of storing data so that it is unalterable.**

![Blockchain](https://i.imgur.com/Wuk0NJ1.png)

So in the case of Bitcoin, the data is a history of monetary transactions. Every so called "block" contains a group of transactions, as well as a special alpha numeric string called a "hash". This hash is essentially a compression of all the data in the block that came before it. It changes drastically if any piece of data is altered.

So what you get is a long line of transactions that very clearly and obviously falls apart if anyone tries to make a change to the history; this is what makes blockchains unalterable or immutable. If you made a transaction yesterday and want to erase it, every block after it would flag the change, because every block after it will be changed. This would then mean that the chain would not be identical to everyone else.

### How does cryptocurrency relate to blockchains?

Cryptocurrency is both an incentive and a means of exchange. The concept of having a nice orderly chain is all nice and good, but it falls apart without a reason for people to keep it this way. Without any consequences to altering blockchains, people still try to alter it somehow.

This is where cryptocurrency comes in. Cryptocurrency is minted only through honest maintenance of the transaction history. When a valid block of transactions is submitted and accepted to the chain, the person who submitted it is rewarded with newly minted cryptocurrency. These people are called miners.

The only way they get a reward is by submitting valid blocks. If you submit a fake or altered block, the other miners will discover it, and earn the reward themselves by submitting the valid block.

## Conclusion

1. **Decentralization** is the core principle behind blockchain technology. It's where you take power from one central authority, and create a better, more robust system by distributing that power to everyone.

2. **Blockchains** are a method of storing data that makes it immutable. Each block stores a hashed version of the data in the previous block, ensuring that no change goes unnoticed.

3. **Cryptocurrency** is the monetary incentive that is built into the network. The blockchain mints new coins for miners that maintain the integrity of the chain's transaction history.


# Code a BlockChain

Every time you have a key and value it's a hashtable. A hashtable is an implementation of a dictionary.

JSON is transported in text through HTTP over the web over API endpoints over REST interfaces but you have to parse it. Takes text rep of JSON, turn it into a hash and puts it in an actual hash table with key and value, but they have to parse it first.

But for these blockchains you do the opposite--you stringify the json key value to text and then you hash that text with the SHA-256 hashing algorithm, which is a deterministic algorithm. It's fast, efficient, and known to have a very even distribution. Hashing cannot be decrypted.

Python hash looks at id of the input to hash and not the actual value.

1 hex bit = 4 bits = 1 nybble

Hexidemical counting system is a base 16 counting system.

256 is 256 bits, which is 64 bytes.

For bitcoin you have to have proof, where the algorithm allows for 256 characters to have 19 leading zeros. The Bitcoin proof-of-work algorithm requires a hash output with 19 leading zeros before a Block is accepted by the network and added to the Bitcoin blockchain.

To guess and check it takes 75 computations per 12 minutes. Every transaction is evaluated every 18 minutes.

Flask is a very light python framework.

UUID is unique user identifier

### Blockchain syntax

1. To create a block string:
   1. You need to convert a python object to a json string

```python
block_string = json.dumps(block, sort_key=True).encode()
```
2. When you retrieve the blockchains it must match everyone else's order. `json.dumps()` is equivalent to `json.stringify()`. In this case, when you retrieve the blockchain dictionary (with `sorted_keys=True), it retrieves it sorted alphabetically, hashed. But if you have it in a different order, the hash will be different even though the data is the same.
3. `encode()`: takes in a python strong which has a wrapper of metadata around it, which prevents it from being hashed
   1. what it does is convert it from a python string into a byte string and strips off all of the metadata, enabling the use of the hash function
   2. in javascript, an array is really an object, and has metadata associated with it, so you can treat it like an object and say
4. Hashing the block with SHA256:
   1. to convert the hash into a readable form--instead of having a hashed object, we want a string of hexidecimal, using `hexdigest()`
   

```python
hash = hashlib.sha256(block_string).hexdigest()
```

#### Review

1. create a dictionary to store our blocks
2. chain will be our python list, or basically an array of our dictionary objects--and that is the BLOCK CHAIN
3. in each block we have:
   1.  an index to let us know how far we are
   2. a timestamp for the transaction ledger
   3. list of transactions
   4. proof, which is the proof of work
   5. previous hash, which, once we make our second block well look at the first block using the hash function
      1. it will turn that block into a string, so JSON.dumps which is the python version of stringify