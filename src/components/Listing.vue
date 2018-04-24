<template>
  <div>

    <div id="upload">
      <Uploader :onUpload="onUpload"></Uploader>
    </div>

    <ul>
      <li v-for="f in sortedFiles">
        {{f.time}} — <a :href="f.url" target="_blank">{{f.name}}</a>
      </li>
    </ul>

  </div>
</template>

<script>
  import Uploader from './Uploader'

  export default {
    name: 'Listing',
    components:{
      Uploader
    },

    data() {
      return {
        files: []
      }
    },

    computed:{
      sortedFiles(){
        return this.files.sort((a,b) => a.time < b.time ? 1 : -1)
      }
    },

    mounted() {

      this.$http.get('http://localhost:7777/files')
        .then(response => {
          this.files = response.body
      }, response => {
          console.error(response)
      })

    },

    methods:{
      onUpload(file){
        console.log('file', file)
        this.files = [...this.files, file]
      }
    }

  }
</script>

<style scoped>
  #upload{
    background: #e1e1e1;
    padding: 20px;
  }
</style>
