<template>
    <div class="noselect">
        <div id="nav-container">
            <nav class="center-h">
                <router-link to="/market"><img id="logo" src="@/assets/logo.png" alt="KeepUp" /></router-link>
                <div class="center-v" id="menu">
                    <ul>
                        <li><router-link class="menu-link graceful" to="/market">Market</router-link></li>
                        <li><router-link class="menu-link graceful" to="/games">Games</router-link></li>
                        <li><router-link class="menu-link graceful" to="/about">About</router-link></li>
                    </ul>
                </div>
                <div class="center-v right">
                    <ul v-if="!isAuthed">
                        <li><router-link class="btn" to="/auth/login">Sign In</router-link></li>
                        <li><router-link class="margin-l btn-inverted" to="/auth/register">Register</router-link></li>
                    </ul>
                    <ul v-else>
                        <li><router-link class="btn" to="/account">{{ Username }}</router-link></li>
                        <li><a @click="logout" class="margin-l btn-inverted">Logout</a></li>
                    </ul>
                </div>
            </nav>
        </div>
    </div>
</template>

<script>

import { mapActions } from 'vuex';

export default {

    computed: {
        isAuthed: function(){ return this.$store.getters.isAuthenticated },
        Username: function(){ return this.$store.getters.User['username'] || "Unknown" }
    },
    
    methods: {
        ...mapActions(['LOGOUT']),

        logout: function() {
            this.$router.go('/auth/login');
            this.LOGOUT();
        },
    }
}

</script>

<style lang="scss" scoped>
  
    @import '@/assets/style/variables.scss';
    
    #nav-container {
        position: fixed;
        width: 100%;
        height: 100px;
        background: $darker;
        z-index: 10000;
    }

    nav {
        width: 1000px;
        height: 100%;
    }
    
    #logo {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        width: auto;
        height: 40%;
        opacity: 0.75;
    }

    #menu {
        position: absolute;
        left: 50%;
        transform: translate(-50%, -50%);
    }

</style>