<template>
  <div class="home">
    <Header />
    <h1>{{ msg }}</h1>
    <strong class="instruccions"
      >Find words entering some of the containing letters:</strong
    >
    <input
      v-model="letters"
      placeholder="YOUR LETTERS"
      class="finder-input block"
    />

    <div>
      <div>
        <input v-model="starts" placeholder="starts with..." class="field" />
        <input v-model="ends" placeholder="ends with..." class="field" />
      </div>
      <div>
        <input v-model="contains" placeholder="contains..." class="field" />
        <input v-model="length" placeholder="lenght..." class="field" />
      </div>
      <button class="search-btn">SEARCH</button>
    </div>
  </div>
</template>

<script>
import Header from "./Header.vue";

export default {
  name: "Home",
  props: {
    msg: String,
  },
  components: {
    Header,
  },
  data: () => ({
    letters: "",
  }),
  computed: () => ({
    "uppercase-letters": () => {
      this.letters.toUppercase();
    },
  }),

  mounted: function () {
    this.letters = "Rellenando on mounted...";
    console.log("letters value: ", this.letters);
  },

  methods: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.home {
  background-color: #42b983;
  color: #ffffff;
}

h1 {
  font-size: 4rem;
}

.instruccions {
  font-size: 1.2rem;
  margin: 1rem;
}

.finder-input {
  font-size: 1.5rem;
  text-align: center;
  text-transform: uppercase;
  padding: 1rem;
  min-width: 25rem;
  border-radius: 25px;
  border-style: none;
  margin: 2rem;
}

.field {
  font-size: 1rem;
  text-align: center;
  padding: 0.5rem;
  width: 15rem;
  border-style: none;
  border-radius: 25rem;
  margin: 1rem;
}

.search-btn {
  font-size: 1rem;
  text-align: center;
  padding: 0.5rem;
  width: 34rem;
  border-style: none;
  border-radius: 25px;
  margin: 1rem;
  background-color: white;
}

.inline {
  display: inline;
}

.block {
  display: block;
  margin-left: auto;
  margin-right: auto;
}


h3 {
  margin: 40px 0 0;
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
