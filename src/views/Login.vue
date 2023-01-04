<template>
    <div>
        <h1 class="text-center text-info">Login Page</h1>
        <div class="col-md-6 offset-md-3">
            <form @submit.prevent="userLogin">
                <div class="mb-3">
                    <label for="email" class="form-label">Email</label>
                    <input type="email" class="form-control rounded-0" id="email" name="email" v-model="userCreditial.email" required minlength="15">
                </div>
                <div class="mb-3">
                    <label for="password" class="form-label">Password</label>
                    <input type="password" class="form-control rounded-0" id="password" name="password" v-model="userCreditial.password" required/> 
                    
                </div>
                <button type="submit" class="btn btn-primary btn-sm float-end">Login</button>
            </form>
        </div>
    </div>
</template>

<script>
import mixins from '../mixins/mixins'
export default{
    mixins:[mixins],
    props:['logged'],
   data(){
        return{
            userCreditial: {
                email:'',
                password:''

            }
        }   
    },
    methods: {
        changeLoginState(){
            this.$emit('changeloginstatus')
        }
    },

    methods:{
        async userLogin(){
          let url=this.$baseUrl+'login';
          let responseData =await this.sendData(url,this.userCreditial);
          if(responseData.con){
            localStorage.setItem('token',responseData.data);
            this.$emit('changeloginstatus')
            this.$router.push({'name':'home'})
          }else{
           alert(responseData.msg);
          }
         
        
        }
       
    }
    
}

</script>