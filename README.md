# For Math Wallet DAPP Developer

## Using Math Wallet Filecoin JS API

### Samples

```

// login
// returns { "name": "test1", "address": "t1u3ynne5fllqpv4re5vkqbvowtsb2aggh2p4u5fa"}
const account = await window.filecoin.login();

// logout
// returns {}
await window.filecoin.logout();

// Sign Transaction
const transaction =  {
        from: this.account.address,
        gasLimit: 10000,
        gasPrice: 1,
        nonce: 0,
        to: "t1uzmmfknk3pq5otq4wosqtzm3oq7675vb27qz6aq",
        value: 1000000000000000000, // 精度18
        method: 0,
        params: ""
      };
await window.filecoin.requestSignature(transaction);

```

For details, please find the sample in this repo.

### Download Math Wallet 麦子钱包下载

[http://mathwallet.org](http://mathwallet.org)


