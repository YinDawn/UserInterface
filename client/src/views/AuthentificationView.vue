<template>
    <div class="view">
            <login-form @triggerState="changeState" v-if="!state"/>
            <registration-form v-if="state" @triggerState="changeState"/>
    </div>
</template>

<script>
    import LoginForm from '../components/LoginForm'
    import RegistrationForm from '../components/RegistrationForm'

    export default {
        name:"AuthentificationView",
        components: {
            "login-form":LoginForm,
            "registration-form":RegistrationForm
        },
        data:()=>{
            return{
                state:true
            }
        },
        methods:{
            changeState(){
                this.state = !this.state;
            }
        },
        created:()=>{

        },
        mounted:()=>{

        }
    }
</script>