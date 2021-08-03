<template>
  <header>
    <router-link to="/">
      <h1>Vue<span>Movie</span></h1>
    </router-link>
  </header>

  <main>
    <router-view/>
  </main>  
</template>

<style lang="scss">
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Fira Sans', sans-serif;

    &::selection {
      background: transparentize(#3F5994, 0.5);
    }
  }

  body {
    background-color: #070606;
  }

  a {
    text-decoration: none;
  }

  header {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 18px 16px;
    background-color: #070606;
    box-shadow: 0px 0px 6px rgba(0,0,0,0.1);

    h1 {
      color: #D7D7D5;
      font-size: 28px;

      span {
        color: #BC4135;
      }
    }
  }
</style>
