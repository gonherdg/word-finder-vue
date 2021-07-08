<template>
  <div class="header">
    <div class="logo">
      <img
        class="logo-img"
        alt="Fast Word Finder"
        src="../assets/logo_black.png"
      />
    </div>
    <!--
    <div class="right-header">
      <div class="option">Word Lists</div>
      <div class="option">Word Finders</div>
    </div>
    -->
  </div>
</template>

<script>
export default {
  name: "Header",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  background-color: #42b983;
}

.logo {
  width: 16rem;
  margin-left: 10%;
}

.logo-img {
  object-fit: cover;
  object-position: center;
  width: 16rem;
  height: 6rem;
}

ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
