<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <router-link to="/" class="navbar-brand"><a>Stock Trader</a></router-link>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <router-link class="nav-item" activeClass="active" tag="li" to="/portfolio"><a class="nav-link">Portfolio</a></router-link>
        <router-link class="nav-item" activeClass="active" tag="li" to="/stocks"><a class="nav-link">Stocks</a></router-link>
      </ul>
      <strong class="navbar-text narbar-right">Funds: {{funds | currency}}</strong>
      <ul class="nav navbar-nav narbar-right">
        <li class="nav-item"><a href="#" class="nav-link" @click="endDay">End Day</a></li>
        <li
          class="nav-item dropdown"
          :class="{show: isDropdownOpen}"
          @click="isDropdownOpen = !isDropdownOpen">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" :aria-expanded="isDropdownOpen">
            Save & Load
          </a>
          <div class="dropdown-menu" :class="{show: isDropdownOpen}" aria-labelledby="navbarDropdown">
            <a class="dropdown-item" href="#" @click="saveData">Save</a>
            <a class="dropdown-item" href="#" @click="loadData">Load</a>
          </div>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  data () {
    return {
      isDropdownOpen: false
    }
  },
  computed: {
    funds () {
      return this.$store.getters.funds
    }
  },
  methods: {
    ...mapActions({
      randomizeStocks: 'randomizeStocks',
      fetchData: 'loadData'
    }),
    endDay () {
      this.randomizeStocks()
    },
    saveData () {
      const data = {
        funds: this.$store.getters.funds,
        stocksPortfolio : this.$store.getters.stocksPortfolio,
        stocks: this.$store.getters.stocks
      }
      this.$http.put('data.json', data)
    },
    loadData () {
      this.fetchData()
    }
  }
}
</script>

<style scoped>
  nav {
    margin: 30px 0;
  }
</style>
