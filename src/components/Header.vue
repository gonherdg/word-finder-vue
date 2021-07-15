<template>
  <div class="header">
    <div class="left-side">
      <img
        class="logo-img"
        alt="Fast Word Finder"
        src="../assets/logo_black.png"
      />
    </div>

    <div class="right-side">
      <router-link class="option" to="/">Home</router-link> |
      <router-link class="option" to="/about">About</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: {
    msg: String,
  },

  methods: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  background-color: #42b983;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  font-family: "Source Sans Pro", sans-serif;
}

.left-side {
  width: 16rem;
  position: left;
  margin-left: 10%;
  text-align: left;
}

.right-side {
  text-align: right;
  position: right;
  margin-right: 10%;
  margin-top: auto;
  margin-bottom: auto;
}

.option {
  padding-left: 1.2rem;
  padding-right: 1.2rem;
  padding-top: 0.6rem;
  padding-bottom: 0.6rem;
  border-radius: 5px;
  border: none;
  background-color: transparent;
  color: black;
  font-size: medium;
  font-weight: 600;
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
