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
        from: this.account.address,//转出账户地址
        gasPremium: "10000",//在app端广播交易时可选,字符串类型
        gasFeeCap:"10000",//在app端广播交易时可选,字符串类型
        nonce: 0,//在app端广播交易时可选,number
        gasLimit: 2200000,//固定即可
        to: "t1uzmmfknk3pq5otq4wosqtzm3oq7675vb27qz6aq",//字符串类型
        value: "1000000000000000000", // 精度18,字符串类型
        method: 0,//固定即可
        params: ""//固定即可
      };
await window.filecoin.requestSignature(transaction);

```

For details, please find the sample in this repo.

### Download Math Wallet 麦子钱包下载

[http://mathwallet.org](http://mathwallet.org)


