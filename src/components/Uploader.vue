<template>
  <div>
    <vue-clip :options="options" :onComplete="uploaded" :onAddedFile="added">
      <template slot="clip-uploader-action">
        <div>{{button}}</div>
      </template>
    </vue-clip>

  </div>
</template>

<script>
  export default {
    name: 'Uploader',

    props: ['onUpload'],

    data: () => ({
      button: 'Click or Drag and Drop files here upload',
      options: {
        url: 'http://localhost:7777/upload',
        paramName: 'file',
        maxFiles: 1
      }
    }),

    methods: {

      added: function () {
        this.button = 'Uploading...'
      },

      uploaded: function (res) {
        const api = JSON.parse(res.xhrResponse.response)
        this.onUpload(api)
        this.button = 'Done !'
        setTimeout(function(){
          this.button = 'Click or Drag and Drop files here upload'
        }, 1500)
      }

    }
  }
</script>
