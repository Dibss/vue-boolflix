<template>
  <div id="tv-container">
    <SearchComp @searchFunction="search"/>
    <!-- per le pagine : @pageSearch="searchPage" :pageArr="pageArr"  -->
    <div id="tv-wall">
      <TvItemComp v-for="film in filmArr" :key="film.id"
        :img="'https://www.themoviedb.org/t/p/original/' + film.poster_path"
        :originalTitle="film.original_title"
        :title="film.title"
        :originalLanguage="film.original_language"
      />
    </div>
    <ItemsFoundComp :items="filmArr.length"/>
  </div>
</template>

<script>
import axios from "axios";
import TvItemComp from "./partials/TvItemComp.vue";
import SearchComp from "./partials/SearchComp.vue";
import ItemsFoundComp from "./partials/ItemsFoundComp.vue"

export default {
name: 'TvWallComp',
components : {
  TvItemComp,
  SearchComp,
  ItemsFoundComp
},
data(){
  return{
    filmArr : [],
    page : 1,
    pageArr : []
  }
},
created(){
  this.getFilm();
  // this.getPage()
},
methods : {
  getFilm(){
    axios.get(`https://api.themoviedb.org/3/search/movie?api_key=1ddea58670cc4bdbfbe9d2d07181ce0c&query=a&page=1`)
      .then((res) => {
        console.log('FILM:', res.data.results);
        this.filmArr = res.data.results
      })
      .catch((error) => {
        console.log(error)
      })
  },
  // per le pagine
  // getPage(){
  //   axios.get(`https://api.themoviedb.org/3/search/movie?api_key=1ddea58670cc4bdbfbe9d2d07181ce0c&query=a`)
  //     .then((res) => {
  //       for(let i = 0; i < res.data.length; i++){
  //         if(this.pageArr.includes(res.data[i].page)){
  //           this.pageArr
  //         } else {
  //           this.pageArr.push(res.data[i].page)
  //         }
  //       }
  //       console.log("PAGES", this.pageArr)
  //     })
  //     .catch((error) => {
  //       console.log(error)
  //     })
  // },
  search( searchedText ){
    this.inputText = searchedText;
    console.log(this.inputText);
    axios.get(`https://api.themoviedb.org/3/search/movie?api_key=1ddea58670cc4bdbfbe9d2d07181ce0c&query=${this.inputText}&page=${this.page}`)
      .then((res) => {
        console.log('FILM:', res.data.results);
        this.filmArr = res.data.results
      })
      .catch((error) => {
        console.log(error)
      })
    this.inputText = ""
  },
  searchPage( page){
    this.selectedPage = page;
    console.log(this.selectedPage);
  },
}
}
</script>

<style scoped lang='scss'>
#tv-container{
  height: 100vh;
  background-color: #434343;
  overflow-y: auto;
  #tv-wall{
    display: flex;
    flex-wrap: wrap;
    width: 80%;
    margin: 2em auto;
  }
}
</style>