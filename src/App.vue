<script>
  import {ref} from 'vue';

  import axios from 'axios';

  export default {
    setup() {


      const blogs = ref('')

      axios.get("https://newsapi.org/v2/everything?q=apple&from=2022-12-24&to=2022-12-24&sortBy=popularity&apiKey=afe532d07ba148329362cacae6343b5e")
        .then(response => {
          blogs.value = response.data
        })
        .catch(error => console.log(error))
      
      return {
        blogs
      }
    }
  }

</script>

<template>
  <header class="header">
    <h1>My Blog</h1>
  </header>

  <main>
    
    <div class="blog">
      <div class="card" v-for="(blog) in blogs.articles" :key="blog.source.id">
        <div class="card-img">
          <img :src='blog.urlToImage' alt="">
        </div>
        <div class="card-body">
          <h6 class="author">
            {{ blog.author }}
          </h6>
          <h3 class="card-title">
            {{ blog.title }}
          </h3>
          <p class="card-text">
            {{ blog.description }}
          </p>
          <a class="btn btn-card" :href="blog.url" target="_blank">Read More</a>
        </div>
      </div>
    </div>
    <!-- {{ blogs.articles[0] }} -->
  </main>

</template>


<style>
  .header {
    background-color: bisque;
    margin-bottom: 20px;
    padding: 30px 50px;
  }
  .header h1 {
    color: black;
    text-transform: uppercase;
    font-size: 2rem;
  }
.blog {
  display: inline-grid;
    grid-template-columns: auto auto;
    padding: 10px;
    gap: 20px;
}

  .card {
    max-width: 500px;
    min-height: 220px;
    height: 100%;
    display: flex;
    padding: 25px 30px;
    margin-left: 50px;
    border-radius: 20px;
    background-color: rgb(60 60 60 / 66%);
    box-shadow: 0px 0px 15px -5px #58585892;
  }

  /* card image style */
  .card-img {
    position: relative;
    inset: 0;
    width: 100%;
    max-width: 120px;
  }
    .card-img img {
      width: 150px;
      height: 180px;
      object-fit: cover;
      position: absolute;
      left: -50%;
      border-radius: 20px;
      box-shadow: 0px 0px 15px -5px rgb(163 163 163)

    }


  /* card body style */
  .card-body {
    width: 100%;
    display: inline-block;
  }

    .card-body .author {
      position: relative;
      inset: 0;
      padding-left: 14px;
      font-size: .9rem;
      color: #dddddd;
      line-height: 1;
    }
    .card-body .author::before {
      content: '';
      position: absolute;
      bottom: 2px;
      left: 0;
      height: 2px;
      width: 12px;
      background-color: #dddddd;
      
    }
    .card-body .card-title {
      color: #f2f2f2;
      font-size: 1.2rem;
      line-height: 1.2;
      overflow: hidden;
      text-overflow: ellipsis;
      display: -webkit-box;
      -webkit-line-clamp: 2;
      line-clamp: 2;
      -webkit-box-orient: vertical;
      margin-top: 5px;
      margin-bottom: 10px;
    }

    .card-text {
      color: #f2f2f2de;
      font-size: .75rem;
      line-height: 1.2;
      margin-bottom: 21px;
      overflow: hidden;
      text-overflow: ellipsis;
      display: -webkit-box;
      -webkit-line-clamp: 3;
      line-clamp: 3;
      -webkit-box-orient: vertical;
    }

  .btn {
    padding: 7px 15px;
    background-color: bisque;
    border-radius: 30px;
    display: inline-block;
    color: rgb(0, 0, 0);
    text-transform: uppercase;
    font-weight: 600;
    font-size: .8rem;
    cursor: pointer;
    text-decoration: none;
    transition: opacity .3s ease-in-out;
  }

  .btn:hover, .btn:focus {
    opacity: .8;
  }
</style>


