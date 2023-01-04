<template>
  <div>
   <div v-if="loaded">
      <slider :cats="cats" :subcats="subcats"/>
      <div v-for="tag in tags" :key="tag.id">
        <h2>
          <span>{{ tag.name }}</span>
          <router-link :to="'/products/pbt/'+tag.id" class="float-end">All</router-link>
        </h2>
        <div class="row">
          <div class="col-md-3" v-for="product in tag.products" :key="product.created">
            <div class="card">
              <img :src="assetUrl+product.images.split(',')[0]" class="card-img-top" alt="" style="max-height:200px">
              <div class="card-body">
              <h5 class="card-title">{{ product.name }}</h5>
              <p class="card-text">{{ product.description }}</p>
              <a href="#" class="btn btn-primary">Go somewhere</a>
            </div>
          </div>
          </div>
        </div>
      </div>
    </div>
    <div v-else class="d-flex justify-content-md-center align-items-center vh-100">
      <div class="loader"></div>
    </div>
 </div> 
</template>

<script>
import mixins from '../mixins/mixins'
import slider from '../components/slider.vue'
export default {
  components: { slider },
  mixins:[mixins],
  data(){
    return {
      subcats:[],
      cats:[],
      tags:[],
      assetUrl:this.$assetUrl,
      loaded:false

    }
  },
  
 async beforeMount(){
    this.cats=await this.loadData(this.$baseUrl+"cats");
    this.tags=await this.loadData(this.$baseUrl+"tags");
    this.subcats=await this.loadData(this.$baseUrl+"subcats");
    for(let tag of this.tags){
      tag.products=await this.loadData(this.$baseUrl+"tag/" +tag.id);

    }
    this.loaded=true;
    // console.log(this.cats);
    // console.log(this.tags);
    // console.log(this.subcats);
   
   }
}
</script>

<style>
.loader{
  width: 120px;
  height: 120px;
  border: 16px solid red;
  border-radius: 50%;
  border-top: 16px solid green;
  animation:spinner 1s linear infinite;
}
@keyframes spinner {
  0%{
    transform: rotate(0deg);
  }
  100%{
    transform: rotate(360deg);
  }
}
</style>

