<template>
    <div class="row mt-5">
        <div class="col-md-3">
            <ul class="list-group">
                <li class="list-group-item rounded-0" v-for="cat in subcats" :key="cat.id">
                    <router-link :to="'/products/pbs/'+cat.id">{{ cat.name }}</router-link>
                </li>
                
            </ul>
        </div>
        <div class="col-md-9">
            <div id="carouselExample" class="carousel slide">
                <div class="carousel-inner">
                    <div class="carousel-item" v-for="(cat,index) in cats " :key="cat.id" :class="{active :index===0}">
                        <img :src="assetsUrl+cat.image" class="d-block w-100" alt="" height="500">
                        <div class="carousel-caption d-none d-md-block">
                            <router-link :to="'/products/pbc/'+cat.id">{{ cat.name }}</router-link>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import mixins from '../mixins/mixins'
    export default {
        mixins:[mixins],
        props:['cats','subcats'],
        data(){
            return {
                assetsUrl:this.$assetsUrl
            }
        }
        
    };

</script>

<style>

</style>