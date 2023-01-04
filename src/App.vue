<template>
  <div>
    <Nav :logged="logged" :cartCount="cartCount" />
    <div class="container-fluid">

      <router-view :logged="logged" @changeloginstatus="loginStatusChange" @changeProductCount="changeProductCount" />
    </div>

  </div>
    
</template>
<script>
import Nav from './components/nav.vue';
export default{
   components:{Nav},
   data(){
      return{
        logged:false,
        cartCount:0
      }
   },
   methods: {
    loginStatusChange(){
      this.logged=!this.logged;
    },
    changeProductCount(){
      let data=localStorage.getItem('products');
      let ary= data ? JSON.parse(data) : [];
      this.cartCount=ary.length;

    },
    beforeMount() {
      this.changeProductCount();
    },
   }
   
   
}
</script>
