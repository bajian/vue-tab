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
      <img src="http://i2.hdslb.com/bfs/archive/33a164cec9e4664675e928c5f0a2844788c077ad.jpg@320w_200h.webp">
      <div>hahaha1</div>
      <div>hahaha1</div>
      <img src="http://i2.hdslb.com/bfs/archive/33a164cec9e4664675e928c5f0a2844788c077ad.jpg@320w_200h.webp">
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
  <br>
  <div>allow different height、verticle scroll</div>
  <b>disable slide below:</b>
  <br>

  <tab :tabtitles="tabtitles2"
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
        'tabtitles':['bajian','github','bajian','github'],
        'tabtitles2':['bajian','github','bajian'],
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
  }

  #app {
    color: #2c3e50;
    margin-top: 50px;
    max-width: 500px;
    width: 100%;
    font-family: Source Sans Pro, Helvetica, sans-serif;
    text-align: center;
    margin: 0 auto
  }


/*TO change the active color u like
    .tab-title.active,.tab-title:active {
        border-bottom: 2px solid #36acf4;
        color: #36acf4;
      }*/
    </style>
