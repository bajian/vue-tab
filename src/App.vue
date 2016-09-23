<template>
  <div id="app">
    <tab :tabtitles="tabtitles" 
    :current-page="3">
    <div class="tab-content-container">
      <button onclick="alert(2)">click</button>
      <div>hahaha1</div>
      <div>hahaha1</div>
      <div>hahaha1</div>
      <div>hahaha1</div>
      <div>hahaha1</div>
      <div>hahaha1</div>
      <div>hahaha1</div>
    </div>
    <div class="tab-content-container">
      bajian2
    </div>
    <div class="tab-content-container">
      bajian3
    </div>
    <div class="tab-content-container">
      bajian4
    </div>
  </tab>

  <br>
  <div>allow different height、verticle scroll</div>
  <b>disable slide:</b>
  <br>

  <tab :tabtitles="tabtitles"
  :slideable="false">
  <div style="height: 200px;background-color: green" class="tab-content-container">
    hahaha1
    <img src="http://i2.hdslb.com/bfs/archive/33a164cec9e4664675e928c5f0a2844788c077ad.jpg@320w_200h.webp">
    <div>hahaha1</div>
    <div>hahaha1</div>
    <img src="http://i2.hdslb.com/bfs/archive/33a164cec9e4664675e928c5f0a2844788c077ad.jpg@320w_200h.webp">
  </div>
  <div style="height: 150px;background-color: #999" class="tab-content-container">
    bajian2
  </div>
  <div class="tab-content-container">
    bajian3
  </div>
  <div class="tab-content-container">
    bajian4
  </div>
</tab>
</div>
</template>

<script>
  import tab from './components/vue-tab'

  export default {
    components: {
      tab
    },
    data(){
      return {
        'tabtitles':['bajian','github','bajian','github']
      }
    }
  }
</script>

<style>
  html {
    height: 100%;
  }

  *{
    margin: 0px;
    padding: 0px;
  }

  body {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
  }

  .tab-content-container{
    width: 99%;
    height: 200px;
    margin: 0px auto;
    /*background-color: #999;*/
  }

  #app {
    color: #2c3e50;
    margin-top: 50px;
    max-width: 500px;
    font-family: Source Sans Pro, Helvetica, sans-serif;
    text-align: center;
  }


/*TO change the active color u like
    .tab-title.active,.tab-title:active {
        border-bottom: 2px solid #36acf4;
        color: #36acf4;
      }*/
    </style>
