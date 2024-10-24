<!-- @input="inputText = $event.target.value" -->
<!-- v-model="inputText"를 사용하면 위와 같은 동작이 수행됨 -->
<!-- @change="inputText = $event.target.value" -->
<!-- @change는 값이 변경되면 실행이 되는것이고 -->
<!-- @v-model(@click)은 변화가 감지되는 순간 실행된다. -->

<template>
  <div>
    <div class="search-box">
      <input
        type="search"
        @change="
          $emit('searchMovie', $event.target.value);
          inputText = $event.target.value;
          $event.target.value = '';
        "
        placeholder="검색어를 입력하세요"
      />
      <button>검색</button>
    </div>
    <p>{{ inputText }}</p>
  </div>
</template>
<script>
export default {
  name: "SearchBarComponent",
  props: {
    data: Array,
  },
  data() {
    return { inputText: "" };
  },
  watch: {
    //트레킹할 변수 명(현재값, 이전값)
    inputText(name) {
      //입력한 영화제목이 데이터에 있는지 확인
      const findName = this.data.filter((movie) => {
        return movie.title.includes(name);
      });
      console.log(findName);
      if (findName.length == 0) {
        alert("해당하는 영화가 없습니다");
      }
    },
  },
};
</script>
<style>
.search-box {
  padding: 10px;
  display: flex;
  justify-content: center;
}

.search-box input {
  padding: 5px 10px;
}
.search-box button {
  margin: 0;
}
</style>
