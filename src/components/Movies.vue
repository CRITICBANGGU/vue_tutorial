<template>
  <div class="container">
    <h1>영화정보</h1>
    <div v-for="(movie, i) in data" :key="i" class="item">
      <figure>
        <!-- (데이터 바인딩)동적인 값을 넣을때 속성 앞에 ':'(콜론)을 넣어야 함. -->
        <img :src="`${movie.imgUrl}`" :alt="`${movie.title}`" />
      </figure>
      <div class="info">
        <!-- :속성명 = "데이터" -->
        <h3 class="bg-yellow">{{ movie.title }}</h3>
        <p>개봉 : {{ movie.year }}</p>
        <p>장르 : {{ movie.category }}</p>
        <!-- 클릭할 때, v-on 속성 사용하면 됨(v-on:이벤트면 ="실행코드") v-on이라고
        안쓰고 그냥 @이로 대체해도 됨 -->
        <!-- <button @:click="increaseLike(i)">좋아요</button> -->
        <button @:click="$emit('increaseLike', i)">좋아요</button>
        <span>{{ movie.like }}</span>
        <p>
          <button @click="$emit('openModal', i)">상세보기</button>
        </p>
      </div>
    </div>
  </div>
</template>
<script>
export default { name: "MoviesComponent", props: { data: Array } };
</script>
<style>
.container {
  padding: 20px;
}
</style>
