<template>
  <div class="header flex flex-row justify-between">
    <div class="flex-1">
      <img
        class="mx-auto object-cover object-center w-64 h-24"
        alt="Fast Word Finder"
        src="../assets/logo_black.png"
      />
    </div>

    <div class="flex-1 my-auto">
      <router-link class="px-3 py-1" to="/">Home</router-link> |
      <router-link class="px-3 py-1" to="/about">About</router-link>
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
  font-family: "Source Sans Pro", sans-serif;
}

.right-side {
  text-align: center;
  position: center;
}

a {
  color: #42b983;
}
</style>
