<template>
    <div class="row my-5">
        <div class="col-md-3" v-for="product in products" :key="product.id">
            <div class="card">
            <img :src="assetUrl+product.images.split(',')[0]" class="card-img-top" alt="" style="max-height:200px">
            <div class="card-body">
                <h5 class="card-title">{{ product.name }}</h5>
                <p class="card-text">{{ product.description }}</p>
                <button href="#" class="btn btn-primary" @click="addToCard(product)"><i class="material-icons">shopping_cart</i></button>
            </div>
        </div>
        </div>
    </div>
</template>

<script>
import mixins from '../mixins/mixins'
export default {
    mixins:[mixins],
    data(){
        return {
         name:null,
         id:null,
         products:[],
         assetUrl:this.$assetUrl
        }
    },
    methods: {
       async loadProduct(){
         let url=this.$baseUrl+this.name+"/"+this.id;
         let response=await this.loadData(url);
         this.products=response.data;
         console.log(this.products);
       },
       addToCard(product){
       let pds=localStorage.getItem('products');
       let pdsAry= pds ? JSON.parse(pds) : [];
       console.log(pdsAry);
        for(pds of pdsAry){
           if(pds.id==product.id) {
            alert("Item Already Exit")
            return;
           }
        }
        pdsAry.push(product);
        console.log(pdsAry);
        localStorage.setItem('products',JSON.stringify(pdsAry));
       }
    
    },

    beforeMount(){
        this.id=this.$route.params.id;
        this.name=this.$route.params.name;
        this.loadProduct();

    },
    
}
</script>