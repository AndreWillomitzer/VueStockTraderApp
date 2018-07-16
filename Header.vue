<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
  <router-link to="/" class="navbar-brand">Stock Trader</router-link>

  <div class="collapse navbar-collapse">
    <ul class="navbar-nav mr-auto">
    <router-link to="/portfolio" activeClass="active" tag="li"><a class="nav-link active">Portfolio</a></router-link>
    <router-link to="/stocks" activeClass="active" tag="li"><a class="nav-link active">Stocks</a></router-link>
    </ul>
    <strong class="navbar-text navbar-right"> Funds: {{ funds | currency }}</strong>
    <ul class="navbar-nav navbar-right">
    <li><a href="#" class="nav-link active" @click="randomizeStocks"> End Day </a></li>
    </ul>
  </div>
  <div class="dropdown">
  <button class="btn btn-light dropdown-toggle"

            type="button"
            id="dropdownMenuButton"
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="false"
            @click="toggleDropdown">

            Save and Load
  </button>
  <div class="dropdown-menu" aria-labelledby="dropdownMenuButton" :class="{show: isDropdownOpen, 'dropdown-menu':true}">
    <a class="dropdown-item" href="#" @click="saveData"> Save Data </a>
    <a class="dropdown-item" href="#" @click="loadData"> Load Data </a>
  </div>
  
</div>
</nav>
</template>

<script>
    import {mapActions} from 'vuex';
    export default {
        data() {
            return {
                 isDropdownOpen: false
        }
        },
        computed: {
            funds() {
                return this.$store.getters.funds;
            }
        },
        methods: {
            ...mapActions({
                randomizeStocks: 'randomizeStocks',
                fetchData: 'loadData'
            }),
            endDay() {
                this.randomizeStocks;
            },
            toggleDropdown(isDropdownOpen) {
                this.isDropdownOpen = !this.isDropdownOpen;
            },
            saveData() {
                const data = {
                    funds: this.$store.getters.funds,
                    stockPortfolio: this.$store.getters.stockPortfolio,
                    stocks: this.$store.getters.stocks
                };
                this.$http.put('data.json', data);
            },
            loadData() {
                    this.fetchData();
            }
        }
    }
</script>