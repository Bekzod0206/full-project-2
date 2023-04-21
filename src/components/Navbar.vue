<template>
  <div class="d-flex flex-column flex-md-row align-items-center py-3 mb-4 border-bottom">
      <a class="d-flex align-items-center text-dark text-decoration-none" >
        <img :src="logo" alt="logo" style="width: 100px; cursor: pointer" @click="toHomeHandler">
      </a>

      <nav class="d-inline-flex mt-2 mt-md-0 ms-md-auto">
        <template v-if="isLoggedIn">
          <Router-link :to="{name: 'create-article'}" class="me-3 py-2 text-dark text-decoration-none">Create article</Router-link>

          <Router-link :to="{name: 'login'}" class="me-3 py-2 text-dark text-decoration-none">{{ currentUser.username }}</Router-link>

          <a href="#" class="me-3 py-2 text-dark text-decoration-none" @click="logout">
            Logout
          </a>
        </template>

        <template v-if="isAnonymus">
          <Router-link :to="{name: 'login'}" class="me-3 py-2 text-dark text-decoration-none">Login</Router-link>
          
          <RouterLink :to="{name: 'register'}" class="me-3 py-2 text-dark text-decoration-none">Register</RouterLink>
      </template>
        
      </nav>
    </div>
</template>

<script>
import { mapState } from 'vuex';
import { mapGetters } from 'vuex'
import { logo } from '../constants';
import { gettersTypes } from '@/modules/types'
export default {
  data(){
    return {logo}
  },
  computed: {
    // ...mapState({
    //   currentUser: state => state.auth.user,
    //   isLoggedIn: state => state.auth.isLoggedIn,
    // }),
    ...mapGetters({
      currentUser: gettersTypes.currentUser,
      isLoggedIn: gettersTypes.isLoggedIn,
      isAnonymus: gettersTypes.isAnonymus
    }),
    // currentUser(){
    //   return this.$store.getters[gettersTypes.currentUser]
    // },
    // isLoggedIn(){
    //   return this.$store.getters[gettersTypes.isLoggedIn]
    // },
    // isAnonymus(){
    //   return this.$store.getters[gettersTypes.isAnonymus]
    // }
  },
  methods: {
    toHomeHandler(){
      return this.$router.push({name: 'home'})
    },
    logout(){
      return this.$store.dispatch('logout')
    }
  }
}
</script>

<style></style>