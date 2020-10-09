<template>
  <div id="app">
    <header class="header">
      <div class="logo">
         <img src="@/assets/senate.png" alt="">
      </div>
      <div class="github">
        <!--<a target="_blank" href="https://github.com/faarda/Nigerian-senators-contacts">
          <img src="@/assets/github.png" alt="">
        </a>-->
		<a target="_blank" href="mailto:silasadedoyin@gmail.com">
		  Built By Silas
        </a>
		&centerdot;
		<a target="_blank" href="https://twitter.com/silasadedoyin">
		  Checkout My Twitter
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
    width: 40px;
  }

  .logo img{
    width: 100%;
  }

  .github{
    display: inline-block;
    /*width: 30px;*/
    cursor: pointer;
	color: #fff;
  }

  .github a{
	  color: #fff;
	  font-size: 14px;
	  font-weight: 700;
  }

  .github img{
    width: 100%;
  }
</style>
