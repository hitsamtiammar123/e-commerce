<template>
    <b-navbar variant="light" fixed="top" type="light" >
      <b-navbar-brand tag="h1" class="mb-0">
          <router-link to="/">
            <img src="/logo.jfif" alt="" class="logo-img">
          </router-link>
      </b-navbar-brand>

      <b-nav-form @submit.prevent="onSearch" right>
        <b-form-input class="mr-sm-2" v-model="search" placeholder="Search"></b-form-input>
        <b-button variant="outline-success" class="my-2 my-sm-0" type="submit">Search</b-button>
      </b-nav-form>
      <b-navbar-nav right  class="ml-auto">
        <router-link to="/login" v-if="!isLogin">
            <b-nav-item href="/login">Login</b-nav-item>
        </router-link>
        <router-link to="/sign-up" v-if="!isLogin">
            <b-nav-item href="/sign-up">Sign-up</b-nav-item>
        </router-link>
          <router-link to="/cart" v-if="isLogin">
            <b-nav-item href="/cart">Cart</b-nav-item>
        </router-link>
        <b-nav-item v-if="isLogin" @click="logout">Logout</b-nav-item>
      </b-navbar-nav>
    </b-navbar>
</template>

<script>
// import {mapActions} from 'vuex'

export default {
    name:'NavBar',
    computed:{
        isLogin(){
            return this.$store.state._isLogin
        },
        searchText(){
            return this.$store.state.searchText
        }
    },
    data(){
        return {
            search:''
        }
    },
    methods:{
       logout(){
           this.$bvModal.msgBoxConfirm('Are You sure want to logout?')
           .then((result)=>{
               if(result){
                    this.$store.dispatch('logout')
                    this.$bvModal.msgBoxOk('See you again')
               }
           })
          
       },
       onSearch(){
           this.$store.state.searchText=this.search
           this.$router.push({name:'Product',query:{search:this.search}})
       }
    }
}
</script>