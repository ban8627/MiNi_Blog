<template>
  <div class="wrap shadow">
    <BlogHeader />
    <BlogInput />
    <BlogList />
    <BlogFooter />
  </div>
</template>

<script>
  import BlogHeader from '@/components/BlogHeader.vue';
  import BlogFooter from '@/components/BlogFooter.vue';
  import BlogList from '@/components/BlogList.vue';
  import BlogInput from '@/components/BlogInput.vue';
  export default {
    components: {
      BlogHeader,
      BlogFooter,
      BlogList,
      BlogInput
    },
    setup() {
      return {}
    }
  }
</script>

<style>
  @charset "utf-8";
  @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@100;300;400;500;700;900&family=Song+Myung&family=Ubuntu:wght@400;500;700&display=swap');

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  ul,
  li {
    list-style: none;
  }

  a {
    text-decoration: none;
    color: #333;
  }

  img {
    border: 0;
    vertical-align: middle;
  }

  html {
    font-size: 16px;
    overflow-x: hidden;
  }

  body {
    font-family: 'Ubuntu', 'Noto Sans KR', sans-serif;
    /* font-family: 'Song Myung', serif; */
    font-size: 14px;
    font-weight: 400;
    line-height: 1.2;
    letter-spacing: -0.64px;
    color:#000;
    background-color: #f6f6f6;
    padding:30px;
  }

  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, .05);
  }

  .wrap {
    position: relative;
    display: block;
    width:90%;
    margin:0 auto;
    border:2px solid rgba(0,0,0,.08);
    border-radius: 10px;
  }
</style>