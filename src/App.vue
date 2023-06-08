<template>
<div class="d-flex flex-column sticky-footer-wrapper">
    <main class="flex-fill">
      <app-header></app-header>
      <message-component></message-component>
      <div class="container mt-3">
          <div class="row">
            <div class="col-md-12">
              <router-view></router-view>
              <div class="card panel-warning d-none d-sm-flex" id="reset-store-panel">
                <div class="card-header">Admin Panel (Testing purpose)</div>
                  <div class="card-body text-center">
                    <button class="btn btn-warning">Reset Store</button>
                  </div>
              </div>
            </div>
          </div>
      </div>
    </main>

    <footer class="navbar-default navbar-bottom navbar-dark bg-dark">
      <div class="container-fluid">
            <p class="text-center nav-bar mb-0">Checkout repository at <a href="https://github.com/ittus/vuejs-firebase-shopping-cart" target="_blank">
              https://github.com/ittus/vuejs-firebase-shopping-cart
            </a></p>
      </div>
    </footer>
</div>

</template>

<script>
  import { mapActions } from 'vuex';
  import Header from './components/Header.vue';
  import MessageComponent from './components/common/MessageComponent.vue';
  export default {
    components: {
      appHeader: Header,
      MessageComponent
    },
    methods: {
      ...mapActions(['getShoppingCart', 'listenToProductList'])
    },
    created() {
      let uid = this.$store.getters.currentUser.uid;
      this.listenToProductList();
      this.getShoppingCart({uid, currentCart: this.$store.getters.cartItemList});
    }
  }
</script>

<style>
  #reset-store-panel {
    position: fixed; bottom: 1px; right: 1px;
  }

  body, .sticky-footer-wrapper {
     min-height:100vh;
  }

  .flex-fill {
     flex:1 1 auto;
  }
  footer {
    height: 100px;
    color: rgb(144, 144, 240);
    padding: 10px 0 10px 0;
    font-size: 90%;
  }
  footer a {
    color: #f19393;
  }
  footer a:hover {
    color: #f19393;
  }
  @media (max-width: 576px) {
    footer {
      height: 50px;
    }
  }
</style> 
