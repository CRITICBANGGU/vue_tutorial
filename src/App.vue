<template>
  <!-- 실제로 html 로 렌더링 되는 곳 -->
    <h1>영화정보</h1>
    <div>
      <!-- :속성명 = "데이터" -->
      <h3 class="bg-yellow" :style="textRed">{{ title }}</h3>
      <p>개봉 : {{ year }}</p>
      <p>장르 : {{ category }}</p>
    </div>
</template>

<script>
export default {
  name: "App",
  //문서에 표시될 변수를 선언할 수 있음 (state)
  data() {
    return {
      title: "노량",
      year: 2023,
      category: "액션, 드라마",
      textRed: "color:red",
    };
  },
};
</script>

<style></style>
<style>
.bg-yellow {
  background-color: gold;
  padding: 10px;
}
</style>
