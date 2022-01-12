<template>
  <div id="app">
    <div class="btn_random">
      <button v-on:click="pedirCotizacion">
      Pedir Contizacion Random
      </button>
    </div>
    <div class="cotizacion">
      <div class="autor">
        <b>{{autor}}</b>
        <p>{{genero}}</p>
      </div>
      <div class="contenido">
        <p>{{texto}}</p>
      </div>
    </div>
  </div>
</template>

<script>

  export default {

    data(){
      return{
        autor: "",
        genero: "",
        texto: ""
      }
    },
    methods:{
      pedirCotizacion(){
        this.$http.get("https://quote-garden.herokuapp.com/api/v3/quotes").then(res =>res.json()).then(res =>{
          let num = Math.random() * (0 -10) + 10;
          let numIndice = Math.round(num);
          this.autor = res.data[numIndice].quoteAuthor;
          this.genero = res.data[numIndice].quoteGenre;
          this.texto = res.data[numIndice].quoteText;
        });
      }
    },
    created(){
        this.$http.get("https://quote-garden.herokuapp.com/api/v3/quotes").then(res =>res.json()).then(res =>{
          let num = Math.random() * (0 -10) + 10;
          let numIndice = Math.round(num);
          this.autor = res.data[numIndice].quoteAuthor;
          this.genero = res.data[numIndice].quoteGenre;
          this.texto = res.data[numIndice].quoteText;
        });
    }
  }

</script>

<style>

  *{
    margin: 0;
    padding: 0;
    background-color: #000;
    color: #fff;
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  .btn_random{
    width: 90%;
    margin-top: 30px;
    text-align: right;
  }

  .btn_random > button{
    cursor: pointer;
    border: none;
    background: transparent;
    font-size: 17px;
  }

  .btn_random > button:hover{
    color: #01f;
  }

  .nada{
    display: none;
  }

  .cotizacion{
    width: 70%;
    margin: auto;
    margin-top: 80px;
  }

  .autor{
    display: inline-block;
    padding: 0 0 5px 20px;
    border-left:2px solid #a0a;
    border-bottom:2px solid #a0a;
  }

  .autor > p{
    margin-top: 5px;
    color: #666;
  }

  .contenido{
    padding: 20px;
    border-left: 2px solid #a0a;
  }


</style>
