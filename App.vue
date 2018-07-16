<template>
    <div class="container">
        <app-header></app-header>
        <div class="row">
            <div class="col-xs-12">
                <transition name="slide" mode="out-in">
                <router-view> </router-view>
                </transition>
            </div>
        </div>
    </div>

</template>

<script>
    import Header from './components/Header.vue';
    export default {
      components: {
        appHeader: Header
      },
      created() {
        this.$store.dispatch('initStocks');
      }
  
    }
</script>

<style>
  body {
    padding: 30px;
  }

  .slide-enter,
    .slide-leave-to {
        opacity: 0;
        transform: translateY(-10px);
    }
    
    .slide-enter-active,
    .slide-leave-active {
        transition: all 0.5s ease-in;
    }

</style>
