<template>
  <div class="home">
    <h1>{{ msg }}</h1>
    <strong class="instruccions"
      >Find words entering some of it's letters:</strong
    >
    <div>
      <div>
        <label>starts with...</label>
        <input
          v-on:change="findWords()"
          v-model="starts"
          placeholder="starts with..."
          class="field"
        />
        <label>ends with...</label>
        <input v-model="ends" placeholder="ends with..." class="field" />
      </div>
      <div>
        <label>contains...</label>
        <input
          v-on:change="findWords()"
          v-model="contains"
          placeholder="contains..."
          class="field"
        />
        <label>it's length...</label>
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

    <div class="words-container" v-if="words !== {} && !justLoaded">
      <ul>
        <li class="word" v-for="(w, key) in words" v-bind:key="key">
          <a
            target="_blank"
            style="color: white"
            :href="'https://www.dictionary.com/browse/' + w.word"
          >
            {{ w.word }}
          </a>
        </li>
      </ul>
    </div>
    <p style="color: #222; margin: 2rem" v-if="!words.length && !justLoaded">
      No words were found.
    </p>
    <div class="some-space"></div>

    <footer>
      <div>
        <div class="f-block">developer: Gonzalo Del Gaudio</div>
        <br />
        <div class="f-block">
          <a style="color: white" href="http://gonsoft.com.ar">www.gonsoft.com.ar</a>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>

import axios from "axios";

export default {
  name: "Home",
  props: {
    msg: String,
  },
  components: {},
  data() {
    return {
      starts: "",
      ends: "",
      contains: "",
      length: 0,
      words: {},
      justLoaded: true,
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
      this.justLoaded = false;
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
  font-size: 3rem;
  margin-top: 0px;
  padding: 1.5rem;
}

.instruccions {
  font-size: 1.2rem;
  margin: 2rem;
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

.words-container {
  margin: 1.5rem;
  padding: 1.5rem;
}

.word {
  padding: 0.4rem;
  background-color: #222;
  border-radius: 10px;
  color: white;
  margin: 0.2rem;
}

.some-space {
  height: 2rem;
  background-color: #42b983;
}

footer {
  padding: 6rem;
  background-color: #222;
}

.f-block {
  margin: 0rem;
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
  color: black;
  text-decoration: none;
}
</style>
