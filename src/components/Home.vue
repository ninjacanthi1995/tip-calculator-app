<template>
  <div class="home">
    <div class="title">
      <h4>SPLI</h4>
      <h4>TTER</h4>
    </div>

    <main>
      <div class="input">

        <div class="bill">
          <label>Bill</label>
          <input type="number" placeholder="0" v-model.lazy="bill" min="0">
        </div>

        <div class="select-tip">
          <label>Select Tip %</label>
          <div class="tips">
            <p v-on:click="tipPercent = 0.05">5%</p>
            <p v-on:click="tipPercent = 0.1">10%</p>
            <p v-on:click="tipPercent = 0.15">15%</p>
            <p v-on:click="tipPercent = 0.25">25%</p>
            <p v-on:click="tipPercent = 0.5">50%</p>
            <input type="number" v-model.lazy="tipCustom" placeholder="Custom" min="0">
          </div>
        </div>

        <div class="people">
          <label>Number of People</label>
          <input type="number" v-model="people" min="0" placeholder="0">
        </div>
      </div>

      <div class="result">
        <div class="result-row">
          <div class="result-title">
            <p>Tip Amount</p>
            <p class="color-dark-grayish-light">/ person</p>
          </div>
          <p>${{ (people ? bill * (!tipCustom ? tipPercent : tipCustom / 100 ) / people : 0).toFixed(2) }}</p>
        </div>

        <div class="result-row">
          <div class="result-title">
            <p>Total</p>
            <p class="color-dark-grayish-light">/ person</p>
          </div>
          <p>${{ (people ? bill * (1 + (tipCustom ? tipCustom / 100 : tipPercent)) / people : 0).toFixed(2) }}</p>
        </div>

        <button>RESET</button>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      tipPercent: null,
      tipCustom: null,
      bill: null,
      people: null,
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  $colorVeryDark: hsl(183, 100%, 15%);
  $colorDarkGrayish: hsl(186, 14%, 43%);
  $colorDarkGrayishLight: hsl(184, 14%, 56%);
  $colorStrong: hsl(172, 67%, 45%);
  $colorLight: hsl(185, 41%, 84%);
  $colorVeryLight: hsl(189, 41%, 97%);

  .home {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: $colorLight;
    font-size: 24px;
    color: $colorVeryDark;
    font-family: 'Space Mono', monospace;
    gap: 2rem;
    padding-top: 2rem;

    .title {
      h4 {
        letter-spacing: 0.5rem;
      }
    }

    main {
      padding: 2rem;
      background-color: white;
      width: 100%;
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
      border-top-left-radius: 1.5rem;
      border-top-right-radius: 1.5rem;
      font-size: 0.9rem;
      font-weight: bold;

      .input {
        display: flex;
        flex-direction: column;
        gap: 1.5rem;

        .bill, .people {
          display: flex;
          flex-direction: column;
        }

        .select-tip {
          display: flex;
          flex-direction: column;
          gap: 1rem;

          .tips {
            display: grid;
            grid-template-columns: repeat(2, minmax(0, 1fr));
            grid-template-rows: 1fr 1fr 1fr;
            width: 100%;
            gap: 1rem;
            font-size: 1.2rem;

            p {
              background-color: $colorVeryDark;
              color: white;
              display: grid;
              place-items: center;
              border-radius: 0.3rem;
            }
          }
        }
      }

      .result {
        width: 100%;
        display: flex;
        flex-direction: column;
        background-color: $colorVeryDark;
        padding: 2rem 1.5rem 1.5rem;
        gap: 1.5rem;
        border-radius: 1rem;

        .result-row {
          display: flex;
          justify-content: space-between;
          align-items: center;
          color: $colorStrong;
          font-size: 1.8rem;

          .result-title {
            color: white;
            font-size: 0.8rem;
          }
        }

        button {
          background-color: $colorStrong;
          color: $colorVeryDark;
          border: none;
          border-radius: 0.3rem;
          padding-block: 0.5rem;
          font-size: 1.1rem;
          font-weight: bold;
        }
      }
    }
  }

  input {
    color: $colorVeryDark;
    border: none;
    background-color: $colorVeryLight;
    padding: 0.5rem 1rem;
    text-align: right;
    border-radius: 0.3rem;
    font-size: 1.2rem;
  }

  .color-dark-grayish-light {
    color: $colorDarkGrayishLight;
  }
</style>
