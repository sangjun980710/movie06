<template>
  <div class="card">
    <a v-bind:href="'https://www.themoviedb.org/movie/'+aa.id">
      <figure>
        <img v-if="aa.poster_path" 
          :src="'https://image.tmdb.org/t/p/w600_and_h900_bestv2' + aa.poster_path" 
          :alt="aa.title">
        <img v-else
          src="http://placehold.it/200x300/ddd/333?text=MoviePoster" 
          :alt="aa.title">
      </figure>
      <div class="text">
        <h3>{{ aa.title }}</h3>
      </div>
    </a>
  </div>
</template>

<script setup>
  const props = defineProps(['aa'])
</script>

<style lang="scss" scoped>
  $tablet: '(max-width:860px)';
  $mobile: '(max-width:600px)';

  .card {   

    width:25%;
    padding:16px;

    @media #{$tablet}{
      width:33.33%;
    }
    @media #{$mobile}{
      width:50%;
    }

    a {
      display: block;
      text-decoration: none;
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 4px 8px rgba(0,0,0,0.3);

      figure{
        width:100%;
        height: 360px;
        margin:0;
        overflow: hidden;        

        img{
          width:100%; 
          height: 100%; 
          object-fit: cover;
          transition: 0.3s;
        }
      }
      .text{
        height:80px;
        padding:16px;

        h3{
          color:#313131;
          font-size: 16px;
        }
      }
    }
    &:hover img { transform: scale(1.1);}
    &:hover a h3 { color:forestgreen}
  }
</style>