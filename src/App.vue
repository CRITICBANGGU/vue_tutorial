<template>
  <!-- 실제로 html 로 렌더링 되는 곳 -->
  <div>
    <h1>영화정보</h1>
    <div>
      <!-- :속성명 = "데이터" -->
      <h3 class="bg-yellow" :style="textRed">{{ title }}</h3>
      <p>개봉 : {{ year }}</p>
      <p>장르 : {{ category }}</p>
    </div>
    <p>{{ foods[0] }}</p>
    <p>{{ foods[1] }}</p>
    <p>{{ foods[2] }}</p>
    <!-- for문 사용하기 "v-for="(아이템, key)in 배열데이터"" -->
    <!-- key 속성 없으면 에러뜸 -->
    <p v-for="(item, i) in foods" :key="i">{{ item }}</p>
  </div>
</template>

<script>
export default {
  name: "App",
  //문서에 표시될 변수를 선언할 수 있음 (state)
  data() {
    return {
      foods: ["김밥", "순대", "만두"],
      title: "노량",
      year: 2023,
      category: "액션, 드라마",
      textRed: "color:red",
    };
  },
};
</script>

<style>
.bg-yellow {
  background-color: gold;
  padding: 10px;
}
</style>
