<template>
<div class="login">
<Navbar/>
  <section class="hero is-success is-fullheight">
        <div class="hero-body">
            <div class="container has-text-centered">
                <div class="column is-4 is-offset-4">
                    <h3 class="title has-text-grey">Create User/Login</h3>
                    <div class="box">
                        <figure class="avatar">
                            <img src="https://placehold.it/128x128">
                        </figure>
                        <form>
                            <div class="field">
                                <div class="control">
                                    <input v-model="email" class="input is-large" type="text" placeholder="Your Email" autofocus="">
                                </div>
                            </div>

                            <div class="field">
                                <div class="control">
                                    <input v-model="name" class="input is-large" type="text" placeholder="Your Name" >
                                </div>
                            </div>
                            <div class="field">
                            
                            </div>
                            <button type="button" @click="login" class="button is-block is-danger is-large is-fullwidth">Login</button>
                        </form>

                    </div>
                    <p class="has-text-grey">
                        <router-link to="/register"><a href="../">Sign Up</a> &nbsp;·&nbsp;</router-link>
                        <a href="../">Forgot Password</a> &nbsp;·&nbsp; 
                        <a href="../">Need Help?</a>
                    </p>
                </div>
            </div>
        </div>
    </section>
  

</div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'

export default {
  name: 'home',
  components: {
    Navbar,
  },
  data:function(){
      return{
          email:'',
          name:''
      }
  },
  methods:{
      login(){
            axios.post('http://35.197.135.159/request-token',{
                email:this.email, 
                name:this.name
                })
               .then(({data})=>{
                   console.log("testing login method")
                   localStorage.setItem('uuid',data.uuid)
                   localStorage.setItem('name',data.name)
                   console.log(data)
                   this.$router.push('/upload')
               })
               .catch(err=>{
                   swal('wrong username/password')
               })
      }
  }
}
</script>

<style>
.hero.is-success {
  background: #F2F6FA;
}
.box {
  margin-top: 5rem;
}
.avatar {
  margin-top: -70px;
  padding-bottom: 20px;
}
.avatar img {
  padding: 5px;
  background: #fff;
  border-radius: 50%;
  -webkit-box-shadow: 0 2px 3px rgba(10,10,10,.1), 0 0 0 1px rgba(10,10,10,.1);
  box-shadow: 0 2px 3px rgba(10,10,10,.1), 0 0 0 1px rgba(10,10,10,.1);
}
input {
  font-weight: 300;
}
p {
  font-weight: 700;
}
p.subtitle {
  padding-top: 1rem;
}
</style>
