<script>
export default {
  data() {
    return {
      marketValue: 0,
      currentBid: 50,
      equalShare4: 0,
      equalShare8: 0,
      minBid: 50,
      maxBid: 0,
      maxProfitBid8: 0,
      maxProfitBid4: 0,
      equalShareGold4: 0,
      equalShareGold8: 0,
      nextPossibleBid: 0,
      shareGold4: 0,
      shareGold8: 0,
      profit: 0,
    };
  },
  mounted() {
    this.calculate();
  },
  methods: {
    calculate() {
      const equalShare8 = this.marketValue * 0.95 * (1 - 1 / 8);
      const maxProfitBid8 = equalShare8 * 0.92 + 1;
      const equalShareGold8 = equalShare8 / 7;

      const shareGold4 = this.currentBid / 3;
      const shareGold8 = this.currentBid / 7;

      const equalShare4 = this.marketValue * 0.95 * (1 - 1 / 4);
      const maxProfitBid4 = equalShare4 * 0.92 + 1;
      const equalShareGold4 = equalShare4 / 3;

      this.maxProfitBid4 = maxProfitBid4.toFixed();
      this.maxProfitBid8 = maxProfitBid8.toFixed();
      this.shareGold4 = shareGold4.toFixed();
      this.shareGold8 = shareGold8.toFixed();
      this.equalShareGold4 = equalShareGold4.toFixed();
      this.equalShareGold8 = equalShareGold8.toFixed();

      this.equalShare4 = equalShare4.toFixed();
      this.equalShare8 = equalShare8.toFixed();

      const maxBid = this.marketValue * 0.95;
      this.maxBid = maxBid.toFixed();
      const profit = this.marketValue * 0.95 - this.currentBid;
      this.profit = profit.toFixed();

      const nextPossibleBid = this.currentBid * 1.1;
      this.nextPossibleBid = nextPossibleBid.toFixed();
    },
  },
};
</script>

<template>
  <div class="card text-bg-dark">
    <div class="card-header">
      <h1>Auction Calculator</h1>
    </div>
    <div class="card-body">
      <form @change="calculate" @keyup="calculate">
        <div class="form-group">
          <div class="row">
            <div class="col">
              <label class="form-label" for="currentBid">Current Bid</label>
              <input
                type="number"
                class="form-control"
                id="currentBid"
                v-model="currentBid"
              />
            </div>
            <div class="col">
              <label class="form-label" for="marketValue">Market Value</label>
              <input
                type="number"
                class="form-control"
                id="marketValue"
                v-model="marketValue"
              />
            </div>
          </div>
        </div>
        <br />
        <div class="form-group">
          <div class="row">
            <div class="col">
              <label class="form-label" for="nextPossibleBid"
                >Next Possible Bid</label
              >
              <input
                disabled
                type="number"
                class="disabled form-control"
                id="nextPossibleBid"
                v-model="nextPossibleBid"
              />
            </div>
          </div>
        </div>
      </form>

      <br />

      <h1>Results</h1>
      <br />
      <h3>Max Bid ( {{ maxBid }}g ) || Profit ( {{ profit }}g )</h3>
      <br />
      <table class="table table-dark table-striped table-condensed">
        <thead>
          <tr>
            <th>#</th>
            <th>Players</th>
            <th>Max Profit Bid</th>
            <th>Equal Bid</th>
            <th>Bid Share</th>
            <th>Equal Share</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>#</td>
            <td>8</td>
            <td>{{ maxProfitBid8 }}g</td>
            <td>{{ equalShare8 }}g</td>
            <td>{{ shareGold8 }}g</td>
            <td>{{ equalShareGold8 }}g</td>
          </tr>
          <tr>
            <td>#</td>
            <td>4</td>
            <td>{{ maxProfitBid4 }}g</td>
            <td>{{ equalShare4 }}g</td>
            <td>{{ shareGold4 }}g</td>
            <td>{{ equalShareGold4 }}g</td>
          </tr>
        </tbody>
      </table>
      <br />
      <h3>Additional Information</h3>
      <ul class="list-group list-group-flush">
        <li class="list-group-item">
          Max Profit Bid is 92% of the Equal Share Bid
        </li>
      </ul>
      <br />
    </div>
  </div>
</template>

<style scoped></style>
