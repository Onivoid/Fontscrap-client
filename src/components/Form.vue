<template>
    <div>
      <input v-model="inputValue" placeholder="Enter some data" />
      <button @click="sendData">Send Data</button>
    </div>
    <div>
        <p v-for="font in fonts">
            {{ font.name }}
        </p>
    </div>
  </template>
  
  <script>
  import axios from 'axios'
  
  export default {
    data() {
      return {
        inputValue: '',
        fonts: []
      }
    },
    methods: {
        async sendData() {
            axios.post('https://fontscrapAPI.skullyfox-tv.fr/scrap', {
                url: this.inputValue
            })
            .then(response => {
                this.fonts = response.data;
                console.log(response.data)
            })
            .catch(error => console.error(error));
        }
  }
}
</script>
 