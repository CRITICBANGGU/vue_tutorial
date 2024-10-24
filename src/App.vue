<template>
  <!-- 실제로 html 로 렌더링 되는 곳 -->
  <div>
    <NavBar />
    <Event :text="text" />
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
        <button @:click="increaseLike(i)">좋아요</button>
        <span>{{ movie.like }}</span>
        <p><button @click="isModal = true">상세보기</button></p>
      </div>
    </div>
    <!-- 조건문 v-if -->
    <div class="modal" v-if="isModal">
      <div class="inner">
        <h3>Detail</h3>
        <p>영화 제목</p>
        <button @click="isModal = false">닫기</button>
      </div>
    </div>
    <Modal
      :data="data"
      :isModal="isModal"
      :selectedMovie="selectedMovie"
      @closeModal="isModal = false"
    />
  </div>
</template>

<script>
import data from "./assets/movies";
import NavBar from "./components/NavBar.vue";
import Modal from "./components/Modal.vue";
import Event from "./components/Event.vue";
export default {
  name: "App",
  //문서에 표시될 변수를 선언할 수 있음 (state)
  data() {
    return {
      isModal: false,
      data: data,
      selectedMovie: 0,
      text: "NETPLIX 강렬한 운명의 드라마, 경기크리처",
    };
  },
  methods: {
    increaseLike(i) {
      this.data[i].like++;
    },
  },
  components: { NavBar: NavBar, Modal: Modal, Event: Event },
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

.modal {
  background: rgba(0, 0, 0, 0.7);
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal .inner {
  background-color: #fff;
  width: 80%;
  padding: 20px;
  border-radius: 10px;
}
</style>
