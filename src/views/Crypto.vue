<script>
import axios from 'axios'

  export default {
    data() {
      return {
        data: [],
        crypto: {},
        loading: false,
      }
    },
    mounted() {
          this.loadData()
    },
    methods: {
      loadData() {
        this.loading = true
        axios.get('https://api.coinstats.app/public/v1/coins?skip=0&limit=10')
            .then(({ data }) => {
                this.data = data.coins
                for (let i = 0; i < this.data.length; i++) {
                    if(this.data[i].id == this.$route.params.id) {
                        this.crypto = this.data[i]
                    }
                }
                this.loading = true
            })
            .catch((error) => {
                this.data = []
                this.loading = true
                throw error
            })
      },
    }
  }
</script>

<template>
  <div v-if="loading">
      <div class="container has-text-centered mt-5">
          <img :src="crypto.icon" alt="" class="image d-block m-auto">
          <h1>Name: {{ crypto.name }}</h1>
          <p>Market cap: {{ crypto.marketCap }}</p>
          <p>Price: {{ crypto.price }}</p>
          <p>Price BTC: {{ crypto.priceBtc }}</p>
          <p>Total Supply: {{ crypto.totalSupply }}</p>
          <p>Symbol: {{ crypto.symbol }}</p>
          <p>Rank: {{ crypto.rank }}</p>
          <p>Twitter URL: {{ crypto.twitterUrl }}</p>
          <p>Website URL: {{ crypto.websiteUrl }}</p>
      </div>
  </div>
</template>

<style>

</style>
