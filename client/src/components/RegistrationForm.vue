<template>
    <div class="component">
        <form @submit.prevent="send">
            <div class="input-container">
                <label>Email</label>
                <br/>
                <input type="mail" placeholder="example@domain.com" v-model="user.email"/>
            </div>
            <div class="input-container">
                <label>Password</label>
                <br/>
                <input type="password" placeholder="******" v-model="user.password"/>
            </div>
            <div class="input-container">
                <label>Confirm Password</label>
                <br/>
                <input type="password" placeholder="******" v-model="user.confirmPassword" />
            </div>
            <div class="input-actions">
                <br/>
                <input type="submit" value="Register" class="btn-reg" v-bind:class="{ active : isActive}" :disabled="!isActive"/>
                <button @click="changeState()" class="text-link">Already registered ? log here :  <i class="fa-solid fa-door-open"></i></button>
            </div>
        </form>
    </div>
</template>

<script>
import '@/css/components/RegistrationForm.css'
export default {
    name:"RegistrationForm",
    data:()=>{
        return{
            user: {
                email:"",
                password:"",
                confirmPassword:""
            },
            emailValid: false,
            passwordValid: false,
            isActive:false
        }
    },
    methods:{
        send(){
            let user = JSON.stringify(this.user);
            this.axios.post("https://localhost:7296/api/User",
            {
                user : user
            })
            .then(response => console.log(response));
        },
        changeState(){
             this.$emit('triggerState');
        },
        checkPassword(password, confirm){
            this.passwordValid = (password !== "" && confirm !== "" ) && (password === confirm) ? true : false;
            this.isActive = this.emailValid && this.passwordValid;
        }
    },
    watch:{
        'user.email'(newValue){
            this.emailValid = newValue !== "" ?  true :  false;
            this.isActive = this.emailValid && this.passwordValid;
        },
        'user.password'(newValue){
            this.checkPassword(newValue,this.user.confirmPassword);
        },
        'user.confirmPassword'(newValue){
            this.checkPassword(this.user.password,newValue);
        }
    }
}
</script>