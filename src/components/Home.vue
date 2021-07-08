<template>
  <div class="home">
    <Header />
    <h1>{{ msg }}</h1>
    <strong class="instruccions"
      >Find words entering some of it's letters:</strong
    >
    <!--
    <input
      v-model="letters"
      placeholder="YOUR LETTERS"
      class="finder-input block"
    />
    -->
    <div>
      <div>
        <input
          v-on:change="findWords()"
          v-model="starts"
          placeholder="starts with..."
          class="field"
        />
        <input v-model="ends" placeholder="ends with..." class="field" />
      </div>
      <div>
        <input
          v-on:change="findWords()"
          v-model="contains"
          placeholder="contains..."
          class="field"
        />
        <input
          v-on:change="findWords()"
          type="number"
          v-model.number="length"
          placeholder="lenght..."
          class="field"
        />
      </div>
      <button v-on:click="findWords()" class="search-btn">SEARCH</button>
    </div>

    <div v-if="words !== {}">
      <ul>
        <li class="word" v-for="(w, key) in words" v-bind:key="key">
          {{ w.word }}
        </li>
      </ul>
    </div>
    <p style="color: black; margin: 2rem" v-if="!words.length">No words were found.</p>
    <div class="some-space"></div>
  </div>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";

export default {
  name: "Home",
  props: {
    msg: String,
  },
  components: {
    Header,
  },
  data() {
    return {
      starts: "s",
      ends: "d",
      contains: "r",
      length: 8,
      words: {},
    };
  },
  computed: () => ({
    "uppercase-letters": function () {
      this.letters.toUppercase();
    },
  }),

  mounted: function () {},

  methods: {
    findWords() {
      console.log(this.starts, this.contains, this.ends, this.length);
      const searchWord = this.starts + "*" + this.contains + "*" + this.ends;
      axios
        .get(`https://api.datamuse.com/words?sp=${searchWord}`)
        .then((response) => (this.words = response.data))
        .then(() => {
          if (this.length)
            return (this.words = this.words.filter(
              (item) => item.word.length === this.length
            ));
          else {
            return this.words;
          }
        });
    },
  },
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

.word {
  padding: 0.4rem;
  background-color: greenyellow;
  border-radius: 10px;
  color: black;
  margin: 0.2rem;
}

.some-space {
  height: 20rem;
  background-color: #42b983;
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
