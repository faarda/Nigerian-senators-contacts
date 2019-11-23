<template>
  <div id="app">
    <header class="header">
      <div class="logo">
         <img src="@/assets/senate.png" alt="">
      </div>
      <div class="github">
        <a target="_blank" href="https://github.com/faarda/Nigerian-senators-contacts">
          <img src="@/assets/github.png" alt="">
        </a>
      </div>
    </header>
    <router-view/>
  </div>
</template>

<style>
  *{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  body{
    font-family: 'Lato', sans-serif;
    color: #001F3F;
  }

  .header{
    background: #008751;
    height: 60px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 20px;
  }

  .logo{
    display: inline-block;
    width: 48px;
  }

  .logo img{
    width: 100%;
  }

  .github{
    display: inline-block;
    width: 30px;
    cursor: pointer;
  }

  .github img{
    width: 100%;
  }
</style>
