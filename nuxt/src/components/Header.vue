<template>
<div class="header_container">
    <div class="header_logo_wrapper">
        <img src="../images/logo.png" alt="" @click="toTop">
    </div>
    <div class="menu_wrapper">
        <p @click="toManageFavorite" v-if="$route.path !== '/manage_favorite'">お気に入り</p>
        <p>{{ user_name }}</p>
        <p @click="signOut">ログアウト</p>
        <input v-if="$route.path === '/'" type="text" v-model="artist_name" placeholder="artist name" @keypress.enter="onSubmit">
    </div>
    
</div>
</template>
<script defer src="https://use.fontawesome.com/releases/v5.15.4/js/all.js"></script>
<style>
    body, h1{
        margin:0;
        padding:0;
    }
    .header_container{
        display: flex;
        justify-content: space-between;
        background: black !important;
        padding:0 40px;
    }
    .header_logo_wrapper{
        color: white;
    }
    .menu_wrapper{
        display: flex;
        align-items: center;
    }
    .menu_wrapper input{
        font-size:20px;
    }
    
    .menu_wrapper p{
        color:white;
        margin-right:30px;
        cursor: pointer;
    }

    .header_logo_wrapper img{
        height:60px;
        cursor: pointer;
    }

    .favo_icon{
        background-color:yellow;
    }
</style>

<script lang="ts">
    import Vue from "vue";

    export default Vue.extend({
        data(){
            return {
                artist_name: "",
                user_name: null
            };
        },
        mounted(){
            this.user_name = this.$store.getters.user.displayName
        },
        methods: {
            onSubmit(){
                this.$emit('searchMusic', this.artist_name);
            },
            signOut(){
                this.$store
                .dispatch('signOut')
                .then(() => {
                    this.$router.push('/login')
                })
            },
            toTop(){
                this.$router.push('/');
            },
            toManageFavorite(){
                this.$router.push('manage_favorite')
            }
        }
    })
</script>
