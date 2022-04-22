<template>
  <div id="header-container">
    <div>
      <h1>boolflix</h1>
    </div>
    <div id="searchbar">
      <input type="text" placeholder="Scrivi il titolo di un film o una serie tv">
      <button>Cerca</button>
    </div>
  </div>
</template>

<script>
export default {
name: 'HeaderComp',
}
</script>

<style scoped lang='scss'>
#header-container{
  background-color: #000;
  height: 8vh;
  max-width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  h1{
    text-transform: uppercase;
    color: red;
    font-weight: 300;
    padding-left: 1em;
  }
  #searchbar{
    flex-basis: 50%;
    margin-right: 1em;
    text-align: right;
    input{
      padding: 0.3em;
      width: 30%;
    }
    button{
      margin-left: 0.5em;
      padding: 0.3em;
    }
  }
}
</style>