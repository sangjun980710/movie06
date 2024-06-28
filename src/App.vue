<template>
  <div class="app">
    <header>
      <h1>The <strong>Movie</strong> Database</h1>
      <form class="search-box" v-on:submit="handleSearch">
        <input 
          type="search"
          class="search-field"
          placeholder="search for a Movie..."
          v-model="search_query"
          >
      </form>
    </header>

    <main>
      <div class="cards">
        <Card v-for="movie in movieList" :aa="movie"/>
        <!-- aa라는 이름으로 movie가 전달됨 -->
      </div>
    </main>

  </div>
</template>

<script setup>
  import { ref } from 'vue';
  import Card from './components/Card.vue'

  const movieList = ref([]);
  const search_query = ref('')


  const handleSearch = async ()=>{
    movieList.value = await fetch(`https://api.themoviedb.org/3/search/movie?query=${ search_query.value}&include_adult=false&language=ko-KR&page=1&api_key=45fcb150351f5049358ecdb91b91b4e0`)
      .then(response => response.json())  
      .then(data =>data.results)

      search_query.value = ''
  }




  const popular = async ()=>{
    movieList.value = await fetch('https://api.themoviedb.org/3/movie/popular?language=ko-KR&page=1&api_key=45fcb150351f5049358ecdb91b91b4e0')
      .then(response => response.json())  //JSON을 입력으로 받아 파싱하여 JavaSript 객체를 생성
      .then(data =>data.results)

      console.log('받아온 데이타- ',movieList.value)
  }

  
popular()


</script>

<style lang="scss">
  $color:#313131;

  * { 
    margin: 0; 
    padding: 0; 
    box-sizing: border-box;
    font-family: sans-serif;
    }
  header {
    padding:50px 0;

    h1 { 
      color:#999;
      text-align: center;
      font-weight: normal;
      text-transform: uppercase;
      font-size: 42px;
      margin-bottom: 30px;

      strong {
        color:$color
      }
    }
  }

  .search-box{
    display: flex;
    justify-content: center;
    padding:0 30px;
    .search-field{
      appearance: none;
      border:none;
      outline:none;
      padding:15px;  
      width:100%;    
      max-width:600px;
      border-radius: 8px;

      font-size: 20px;
      color:$color;
      background-color: #f3f3f3;
      box-shadow: 0 4px 8px rgba(0,0,0,0.3);

      &::placeholder{
        color:#aaa;
      }

      &:focus {
        background: $color;
        color:#fff
      }

    }
  }

  main{
    max-width: 1200px;
    margin: auto;
    padding: 0 16px;

    .cards{
      display: flex;
      flex-wrap: wrap;
    }
  }


</style>