<template>
  <div id="items">
    <span>Found {{items}} items</span>
  </div>
</template>

<script>
export default {
name: 'ItemsFoundComp',
props : {
  items : Number
}
}
</script>

<style scoped lang='scss'>
#items{
  text-align: center;
  color: #fff;
  font-weight: 700;
  margin: 2em;
  flex-basis: 100%;
}
</style>