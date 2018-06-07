<template>
<div class="navbarandmodal">

<nav class="navbar is-transparent">
  <div class="navbar-brand">
    <a class="navbar-item" href="">
      <router-link to="/home"><img src="../assets/logosmall.png" alt="HelloKitty" width="112" height="28"></router-link>
    </a>
    <div class="navbar-burger burger" data-target="navbarExampleTransparentExample">
      <span></span>
      <span></span>
      <span></span>
    </div>
  </div>  

  <div id="navbarExampleTransparentExample" class="navbar-menu">
    <div class="navbar-start">

    </div>

    <div class="navbar-end">
      <div class="navbar-item">
        <div class="field is-grouped">
           <p  class="control">
            <button v-if="this.uuid!==null" aria-haspopup="true" class="button">
              <span><router-link to="/home">See All Images</router-link></span>
            </button>
          </p>
          <p v-if="this.uuid==null" class="control">
            <button aria-haspopup="true" class="button">
              <span><router-link to="/">Login</router-link></span>
            </button>
          </p>
          <p  v-if="this.uuid!==null" class="control">
            <button @click="logout" aria-haspopup="true" class="button">
              <span><router-link to="/">Logout</router-link></span>
            </button>
          </p>
        </div>
      </div>
    </div>
  </div>
</nav>

</div>  
</template>

<script>

import { mapActions, mapState} from 'vuex'

export default {
  created:function(){
    this.checkLocalStorage()
  },
  data:function(){
    return{
      uuid:'',
    }
  },
  methods:{
    ...mapActions([
      'getCart','filterCart'
    ]),
    logout(){
      localStorage.clear()
      this.$router.push('/')
    },
    checkLocalStorage(){
      this.uuid=localStorage.getItem('uuid')
    },
  }
}
</script>

<style scoped>

#logoutbutton{
  color:black !important
}

#registerbutton{
  color:black !important
}

</style>


