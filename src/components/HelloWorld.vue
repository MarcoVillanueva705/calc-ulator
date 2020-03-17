<template>
  <div class="calculator">
    <form @submit.prevent="calculate">
    <input type="number" placeholder="amount" v-model="newCalc.balance">
    <input  type="number" placeholder="interest rate" v-model="newCalc.pmt">
    <select id="rates" name="Term">
      <option value="15">15</option>  
      <option value="30">30</option>
    </select>
    <button type="submit">Calculate</button>
    </form>

    <h2>Total Balance</h2><span>{{newCalc.balance}}</span>
    <h2>Monthly Payment</h2><span>{{newCalc.pmt}}</span>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data() {
    return {
      newCalc: {
        balance: 0,
        pmt: 0,
      }
    };
  },

  methods: {
    
  calculate(amount, interest, term) {
  // let calc = { ...this.newCalc };
  if (!amount || !interest || !term) return { balance: 0, pmt: 0 };

  // Total loan cost in a fixed mortage is:
  // r * p * n / (1 - (1 + r)^-n)

  // where r = interest rate / 12
  // n = number of payments or term * 12
  // p = principal

  const r = (interest * 0.01) / 12;
  const n = term * 12;
  const p = amount;

  const balance = ((r * p * n) / (1 - Math.pow(1 + r, -n))).toFixed(2);
  const pmt = (balance / n).toFixed(2);
  // this.newCalc = { balance:0, pmt:0};

  // Uncomment for debug output
  // console.log({ amount, interest, term });
  // console.log({ balance, pmt });



  return {
balance,
pmt
};
} 
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
