<template>
<div id="admin">
<Navbar/>

<!--CONTENT-->
<div class="content">

Input 1:
<div class="field container">
  <div class="control">
    <input  class="input is-link" type="text" placeholder="Buat hiasan aja">
  </div>
</div>


Input 2:
<div class="field container">
  <div class="control">
    <input  class="input is-link" type="text" placeholder="Buat Hiasan 2">
  </div>
</div>
        <!--FILE UPLOAD-->

            <div class="file has-name container">
                <label class="file-label">
                    <input  @change="previewFile" class="file-input" type="file" name="resume">
                    <span class="file-cta">
                    <span class="file-icon">
                        <i class="fas fa-upload"></i>
                    </span>
                    <span class="file-label">
                        Choose a file…
                    </span>
                    </span>
                    <span class="file-name">
                    {{this.filename}}
                    <!-- <button type="button" class="button">Upload</button> -->
                    </span>
                </label>
                <div id="output"></div>
            </div>
            

        <!--FILE UPLOAD END-->
<button  @click="uploadPic" type="button" class="button is-link">Upload</button>

</div>
<!--CONTENT END-->

</div>
</template>


<script>

import Navbar from '@/components/Navbar.vue'

export default {
  name: 'admin',
  data:function(){
      return{
          formdata : new FormData(),
          filename:'',
      }
  },
  components: {
    Navbar,
  },
  methods:{
      previewFile(file){
          console.log({Event})
          var filedata = file.target.files[0]
          this.filename = filedata.name
          this.formdata.append('file',filedata)    
      },
      uploadPic(){
          var getuuid = localStorage.getItem('uuid')
          console.log(getuuid)
           const config = {
                headers: { 
                    'authorization': getuuid,
                    'content-type': 'multipart/form-data' }
            }
            axios.post("http://35.197.135.159/image",this.formdata,config)
            .then(({data})=>{
                console.log("masukkkk ga disini")
                console.log("data",data) 
            })
            .catch(err=>{
                console.log('errorzzzz')
                console.log(err)
            })
      },

  }
}
</script>

<style>
.content{
    padding-top: 40px;
}

</style>



