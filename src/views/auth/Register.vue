<template>
    <div class="content fade-in">
        <div id="auth">
            <h1>REGISTER</h1>
            <p>Sign up at <strong>KeepUp</strong> to see your Steam inventory's true value.</p>
            <div class="message-box"><p :class="{ 'error' : error }">{{ error }}</p></div>
            <div id="auth-form" :class="{ 'disabled' : this.submitted }">
                <form @submit.prevent="submit">
                    <input placeholder="Email" type="text" v-model="form.email">
                    <input placeholder="Choose Password" type="password" v-model="form.choosePassword">
                    <input class="space" placeholder="Repeat Password" type="password" v-model="form.repeatPassword">
                    <button class="btn large" type="submit">Register</button>
                </form>
                <router-link class="btn-inverted large" to="/auth/login">Sign in</router-link>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'Register',

    data() {
        return {
            submitted: false,
            error: null,
            form: {
                email: '',
                choosePassword: '',
                repeatPassword: ''
            }
        }
    },

    methods: {
        submit: function() {
            this.submitted = true;
            this.error = null;

            this.$store.dispatch('REGISTER', {
                'email': this.form.email,
                'password': {
                    'first': this.form.choosePassword,
                    'second': this.form.repeatPassword
                }
            })
            .then(() => { this.$router.push('/auth/steam') })
            .catch(err => { this.error = err.response ? err.response.data.error : err })
            .finally(() => { this.submitted = false })
        },
    },
}

</script>

<style lang="scss" scoped>
    
    #auth {
        position: relative;
        height: 450px;
        width: 30%;
        left: 50%;
        top: 35vh;
        transform: translate(-50%, -50%);
    }

    #auth-form {
        position: absolute;
        width: 100%;
        bottom: 0;
    }

</style>