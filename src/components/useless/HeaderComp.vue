<template>
  <div id="header-container">
    <div>
      <h1>boolflix</h1>
    </div>
    <SearchComp/>
  </div>
</template>

<script>
import SearchComp from "../partials/SearchComp.vue"

export default {
name: 'HeaderComp',
components : {
  SearchComp
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
}
</style>