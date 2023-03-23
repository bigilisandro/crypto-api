<script>
import axios from 'axios'

  export default {
    data() {
      return {
        data: [],
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
                console.log(data)
                this.loading = true
                this.data = data.coins
                this.loading = false
            })
            .catch((error) => {
                this.data = []
                this.loading = false
                throw error
            })
      },
      selectRow(data) {
        this.$router.push({ name: 'crypto', params: { id: data.id } })
      }
    }
  }
</script>

<template>
  <div>
    <div>
      <b-table
        :data="data"
        striped
        hoverable
        :loading="loading"
        @click="selectRow">

        <b-table-column field="rank" label="Rank" width="20" sortable numeric v-slot="props">
            {{ props.row.rank }}
        </b-table-column>

        <b-table-column field="icon" label="Icon" width="200" centered sortable numeric v-slot="props">
          <img :src="props.row.icon" alt="" class="image is-32x32 d-block m-auto">
        </b-table-column>

        <b-table-column field="name" label="Name" searchable v-slot="props">
            {{ props.row.name }}
        </b-table-column>

        <b-table-column field="symbol" label="Symbol" v-slot="props">
            {{ props.row.symbol }}
        </b-table-column>

        <b-table-column field="price" label="Price" centered v-slot="props">
            {{ props.row.price }}
        </b-table-column>

      </b-table>
    </div>
  </div>
</template>

<style>

</style>

