<template>
  <!-- 실제로 html 로 렌더링 되는 곳 -->
  <div>
    <NavBar />
    <Event :text="text" />
    <SearchBar :data="data_temp" @searchMovie="searchMovie($event)" />
    <button @click="showAllMovies()">전체보기</button>
    <Movies
      :data="data_temp"
      @openModal="
        isModal = true;
        selectedMovie = $event;
      "
      @increaseLike="increaseLike($event)"
    />
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
import Movies from "./components/Movies.vue";
import SearchBar from "./components/SearchBar.vue";
export default {
  name: "App",
  //문서에 표시될 변수를 선언할 수 있음 (state)
  data() {
    return {
      isModal: false,
      data: data,
      data_temp: [...data], //사본
      selectedMovie: 0,
      text: "NETPLIX 강렬한 운명의 드라마, 경기크리처",
    };
  },
  methods: {
    increaseLike(id) {
      // this.data[i].like++;
      this.data.find((movie) => {
        if (movie.id == id) {
          movie.like += 1;
        }
      });
    },
    searchMovie(title) {
      //영화 제목이 포함된 데이터를 가져오기
      this.data_temp = this.data.filter((movie) => {
        return movie.title.includes(title);
      });
    },
    showAllMovies() {
      this.data_temp = [...this.data];
    },
  },
  components: {
    NavBar: NavBar,
    Modal: Modal,
    Event: Event,
    Movies: Movies,
    SearchBar: SearchBar,
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
