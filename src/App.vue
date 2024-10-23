<template>
  <!-- 실제로 html 로 렌더링 되는 곳 -->
  <div>
    <h1>영화정보</h1>
    <div v-for="(movie, i) in data" :key="i" class="item">
      <figure>
        <!-- 동적인 값을 넣을때 속성 앞에 ':'(콜론)을 넣어야 함. -->
        <img :src="`${movie.imgUrl}`" :alt="`${movie.title}`" />
      </figure>
      <div class="info">
        <!-- :속성명 = "데이터" -->
        <h3 class="bg-yellow" :style="textRed">{{ movie.title }}</h3>
        <p>개봉 : {{ movie.year }}</p>
        <p>장르 : {{ movie.category }}</p>
        <!-- 클릭할 때, v-on 속성 사용하면 됨(v-on:이벤트면 ="실행코드") v-on이라고
        안쓰고 그냥 @이로 대체해도 됨 -->
        <button @:click="increaseLike(i)">좋아요</button>
        <span>{{ movie.like }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  //문서에 표시될 변수를 선언할 수 있음 (state)
  data() {
    return {
      data: [
        {
          title: "노량",
          year: 2023,
          category: "액션, 드라마",
          textRed: "color:red",
          like: 0,
          imgUrl: "./assets/노량.webp",
        },
        {
          title: "아쿠아맨과 로스트 킹덤",
          year: 2023,
          category: "액션, 판타지, 어드벤처",
          like: 0,
          imgUrl: "./assets/아쿠아맨.webp",
        },
        {
          title: "3일의 휴가",
          year: 2023,
          category: "판타지, 드라마",
          like: 0,
          imgUrl: "./assets/3일의휴가.webp",
        },
      ],
    };
  },
  methods: {
    increaseLike(i) {
      this.data[i].like++;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
}
body {
  max-width: 768px;
  margin: 0 auto;
  padding: 20px;
}

h1,
h2,
h3 {
  margin-bottom: 1rem;
}
p {
  margin-bottom: 0.5rem;
}
button {
  margin-right: 10px;
  margin-top: 1rem;
}
.item {
  width: 100%;
  border: 1px solid #ccc;
  display: flex;
  margin-bottom: 20px;
  padding: 1rem;
}
.item figure {
  width: 30%;
  margin-right: 1rem;
}

.item img {
  width: 100%;
}

.item .info {
  width: 100%;
}

.bg-yellow {
  background-color: gold;
  padding: 10px;
}
</style>
