<template>
    <div class="logo">
      <img src="../assets/logo_w.png" alt="Logo FontScrap">
    </div>
    <div class="form">
      <div class="button clear" @click="delInput">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512">
          <path d="M310.6 150.6c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0L160 210.7 54.6 105.4c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3L114.7 256 9.4 361.4c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0L160 301.3 265.4 406.6c12.5 12.5 32.8 12.5 45.3 0s12.5-32.8 0-45.3L205.3 256 310.6 150.6z"/>
        </svg>
      </div>
      <div class="button send" @click="sendData">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
          <path d="M438.6 278.6c12.5-12.5 12.5-32.8 0-45.3l-160-160c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3L338.8 224 32 224c-17.7 0-32 14.3-32 32s14.3 32 32 32l306.7 0L233.4 393.4c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0l160-160z"/>
        </svg>
      </div>
      <input v-model="inputValue" placeholder="Exemple : https://facebook.com" />
    </div>
    <div class="list">
      <ul>
        <li v-if="this.fonts[0]">
          <span class="notes">
            Voici la liste des fonts utilisées par le site <a v-bind:href="inputValue" target="_blank"> {{ this.inputValue }} </a>
          </span>
        </li>
        <li v-for="font in fonts">
          <p class="fonts">
            {{ font.name }}
          </p>
        </li>
        <li v-if="this.fonts[0]">
          <span class="notes">
           Une grande partie des fonts listées ci-dessus peuvent être trouvé sur le site <a href="https://fonts.google.com" target="_blank">Google Fonts</a>
          </span>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
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
        },
        delInput() {
          this.inputValue = ''
          this.fonts = []
        }
  }
}
</script>

<style scoped>
  .logo{
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .logo img{
    width: 300px;
  }
  input{
    font-family: 'Montserrat';
    outline: none;
    padding: 10px;
    width: 350px;
    font-size: 18px;
    height: 50px;
  }
  .button{
    display: flex;
    align-items: center;
    width: max-content;
    height: 50px;
    padding: 10px;
    font-family: "Montserrat";
    font-weight: bold;
    font-size: 18px;
    color: #fafafa;
    transition: all .3s;
    margin: 0 10px;
  }
  .send {
    background-color: #00a8ff;
    transition: width 3s;
  }
  .clear{
    background-color: #e84118;
    transition: width 3s;
  }
  svg {
    fill: #fafafa;
    margin: 0 10px;
    width: 20px;
    transition: all .3s;
  }
  .button:hover{
    cursor: pointer;
  }
  .send:hover{
    filter: drop-shadow(0 0 0.75rem #00a8ff);
  }
  .clear:hover{
    filter: drop-shadow(0 0 0.75rem #e84118);
  }
  .send:hover::before{
    content: 'Récupérer les Polices';
  }
  .clear:hover::before{
    content: 'Supprimer le lien';
  }
  .button:hover svg{
    transform: rotate(180deg);
  }
  .form{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
  }
  .list{
    display: flex;
    justify-content: flex-start;
    align-items: center;
    margin: 10px 0;
  }
  .list ul{
    list-style: none;
    padding: 0 10px;
  }
  .list li {
    text-align: center;
    font-size: 20px;
  }
  .list li .fonts{
    font-size: 25px;
  }
  .notes{
    font-weight: bold;
  }

</style>
 