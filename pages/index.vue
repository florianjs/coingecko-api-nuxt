<template>
  <div>
    <Chart v-if="show" :dataBTC="key" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      key: [],
      show: false,
    }
  },

  created() {
    this.$axios
      .get(
        'https://api.coingecko.com/api/v3/coins/bitcoin/market_chart?vs_currency=usd&days=300'
      )
      .then((response) => {
        let chart = []
        const data = response.data.prices

        data.forEach((element) => {
          chart.push({
            time: element[0] / 1000,
            value: element[1],
          })
        })
        this.key = chart
        this.show = true
      })
  },
}
</script>
