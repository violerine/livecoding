<template>
  <div class="home">
    <Navbar/>
    <div v-for="(image,index) in images" :key="index" class="images">
      <p>{{image.user.name}}</p>
      <img :src=image.url>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Navbar from '@/components/Navbar.vue'

export default {
  name: 'home',
  created:function(){
    this.getAllImages()
  },
  data:function(){
    return{
      images:''
    }
  },
  components: {
    HelloWorld,
    Navbar

  },
  methods:{
    getAllImages(){
      var getuuid=localStorage.getItem('uuid')
      const config = {
        headers: { 
          'authorization': getuuid }
      }
      axios.get("http://35.197.135.159/image",config)
      .then(({data})=>{
        console.log("IMAGES DATA",data)
        this.images=data
      })
      .catch(err=>{
        console.log("error")
      })
    }
  },
}
</script>
