<template>
    <div class="component">
        <form @submit.prevent="send">
            <div class="input-container">
                <label>Email</label>
                <br/>
                <input type="mail" placeholder="example@domain.com" v-model="user.email" />
            </div>
            <div class="input-container">
                <label>Password</label>
                <br/>
                <input type="password" placeholder="******" v-model="user.password" />
            </div>
            <div class="input-actions">
                <br/>
                <input type="submit" value="Log"  :disabled="!isActive" class="btn-log"/>
                <button @click="changeState()" class="text-link">Not already registered ? click here :  <i class="fa-solid fa-right-to-bracket"></i></button>
            </div>
        </form>
    </div>
</template>

<script>
    export default {
        name:"LoginForm",
        data:() => {
            return{
                user: {
                    email:"",
                    password:"",
                },
                emailValid: false,
                passwordValid: false,
                isActive:false
            }
        },
        methods:{
            send(){
                // call api
                console.clear();
                let user = JSON.stringify(this.user);
                console.log(user);
            },
            changeState(){
                this.$emit('triggerState');
            }   
        },
        watch:{
        'user.email'(newValue){
            this.emailValid = newValue !== "" ?  true :  false;
            this.isActive = this.emailValid && this.passwordValid;
        },
        'user.password'(newValue){
            this.passwordValid = (newValue !== "" ) ? true : false;
            this.isActive = this.emailValid && this.passwordValid;
        }
    }
}
</script>