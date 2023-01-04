<template>
    <div>
        <h1 class="text-center text-info">Register Page</h1>
        <div class="col-md-6 offset-md-3">
            <form @submit.prevent="userRegister">
                <div class="row">
                    <div class="col-md-6">
                      <div class="mb-3">
                            <label for="name" class="form-label">Name</label>
                            <input type="text" class="form-control rounded-0" id="name" name="name" v-model="userCreditial.name" required pattern="[a-zA-Z]{6,}+" 
                            oninvalid="this.setCustomValidity('Error Message')" >
                      </div>
                    </div>
                    <div class="col-md-6">
                        <div class="mb-3">
                            <label for="email" class="form-label">Email</label>
                            <input type="email" class="form-control rounded-0" id="email" name="email" v-model="userCreditial.email" required minlength="15">
                        </div>
                    </div>
                    <div class="col-md-6">
                        <div class="mb-3">
                            <label for="name" class="form-label">Phone</label>
                            <input type="tel" class="form-control rounded-0" id="phone" name="phone" v-model="userCreditial.phone" required pattern="[0-9]{6,11}">
                        </div>
                    </div>
                    <div class="col-md-6">
                        <div class="mb-3">
                            <label for="password" class="form-label">Password</label>
                            <input type="password" class="form-control rounded-0" id="password" name="password" v-model="userCreditial.password" required
                            pattern="^(?=.*\d)(?=.*[!@#$%^])(?=.*[a-z])(?=.*[A-Z]).{8,}$" oninvalid="this.setCustomValidity('Error Message')">
                            
                        </div>
                    </div>
                    <div class="col-md-6">
                        <div class="mb-3">
                            <label for="password2" class="form-label">Confirmation Password</label>
                            <input type="password" class="form-control rounded-0" id="password2" name="password2" v-model="userCreditial.password2" required
                            pattern="^(?=.*\d)(?=.*[!@#$%^])(?=.*[a-z])(?=.*[A-Z]).{8,}$" oninvalid="this.setCustomValidity('Error Message')">
                        </div>
                    </div>
                    <div class="col-md-6 mt-4">
                        <button type="submit" class="btn btn-primary btn-sm float-end mt-3">Register</button>
                    </div> 
                </div>
            
            </form>
        </div>
    </div>
</template>

<script>
import mixins from '../mixins/mixins';
export default {
    mixins:[mixins],
    data(){
        return {
            userCreditial:{
                name:"",
                email:"",
                phone:"",
                password:"",
                password2:""          
            }
        }
    },
    methods:{
        async userRegister(){
            let responseData=await this.sendData(this.$baseUrl+"register",this.userCreditial);
          if(responseData.con){
            this.$router.push({name:'Login'})
          }else{
            //change to dialog
            alert(responseData.msg);
          }
        },
    }
}

</script>