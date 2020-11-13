<template>
  <v-app>
    <v-content>
      <v-container fluid>
        <v-card light>
          <v-card-title>{{account?account.name:"Open MathWallet"}}</v-card-title>
          <v-card-subtitle>{{account?account.address:""}}</v-card-subtitle>
          <v-card-actions>
            <v-btn class="primary" @click="login" v-if="!account">Log in</v-btn>
            <v-btn class="warning" @click="logout" v-else>Log out</v-btn>
          </v-card-actions>
        </v-card>

        <v-card light class="mt-2" v-if="account">
          <v-card-title>Transaction</v-card-title>
          <v-card-subtitle>{{txId?txId:""}}</v-card-subtitle>
          <v-card-actions>
            <v-btn class="success" @click="sendTransaction">Transaction</v-btn>
          </v-card-actions>
        </v-card>
        <v-card light class="mt-2" v-if="account">
          <v-card-title>Signature</v-card-title>
          <v-card-subtitle>{{signature?JSON.stringify(signature):""}}</v-card-subtitle>
          <v-card-actions>
            <v-btn class="success" @click="requestSignature">Signature</v-btn>
          </v-card-actions>
        </v-card>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      account: null,
      txId: null,
      signature: null
    };
  },
  methods: {
    logout() {
      window.filecoin.getAccount().then(() => {
        this.account = null;
      });
    },
    login() {
      if (!window.filecoin) {
        alert("Please install MathWallet first!");
        return;
      }
      window.filecoin.getAccount().then(account => {
        this.account = account;
      });
    },
    requestSignature(){
      if (!this.account) {
        alert("Please log in first!");
        return;
      }
      let transaction = {
        from: this.account.address,
        gasPremium: "10000",
        gasFeeCap: "10000",
        gasLimit:2200000,
        nonce: 0,
        to: "t1uzmmfknk3pq5otq4wosqtzm3oq7675vb27qz6aq",
        value: "1000000000000000000", // 精度18
        method: 0,
        params: ""
      };
      window.filecoin.sendTransaction(transaction).then(signature => {
        this.signature = signature;
      });
    },
    sendTransaction() {
      if (!this.account) {
        alert("Please log in first!");
        return;
      }
      let transaction = {
        from: this.account.address,
        gasPremium: "10000",//可选
        gasFeeCap: "10000",//可选
        gasLimit:2200000,
        nonce: 0,//可选
        to: "t1uzmmfknk3pq5otq4wosqtzm3oq7675vb27qz6aq",
        value: "1000000000000000000", // 精度18
        method: 0,
        params: ""
      };
      window.filecoin.sendTransaction(transaction).then(txId => {
        this.txId = txId;
      });
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
