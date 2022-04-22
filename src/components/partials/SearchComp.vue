<template>
  <div id="header-container">
    <div>
      <h1>boolflix</h1>
    </div>
    <div id="searchbar">
      <form action="" class="d-flex">
        <input type="text"
          placeholder="Scrivi il titolo di un film o una serie tv"
          v-model="inputText"
        >
        <button type="submit" @click.prevent="$emit( 'searchFunction', inputText )">Cerca</button>
        <!-- <select name="page" id="page" @click.prevent="$emit( 'pageSearch', selectedPage )" v-model="selectedPage">
          <option :value="page" v-for="page in pageArr" :key="page.id">{{page}}</option>
        </select> -->
      </form>
    </div>
  </div>
</template>

<script>

export default {
name: 'SearchComp',
data(){
  return{
    inputText : "",
    pageArr : Array
  }
}
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
    form{
      display: flex;
      justify-content: flex-end;
    }
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