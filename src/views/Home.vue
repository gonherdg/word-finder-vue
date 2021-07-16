<template>
  <div class="home flex flex-col">
    <div class="content h-full" :class="{ 'min-h-screen': this.justLoaded }">
      <h1 class="text-3xl sm:text-5xl my-10 p-1 px-6">Fast Word Finder</h1>
      <div class="m-2">
        <strong class="text-lg px-6"
          >Find words entering some of it's letters:</strong
        >
      </div>
      <div class="flex flex-col sm:flex-row justify-around">
        <div class="flex flex-col mx-auto sm:ml-auto sm:mr-4 md:mr-8">
          <label class="mt-4">starts with...</label>
          <input
            v-on:change="findWords()"
            v-model="starts"
            placeholder=""
            class="rounded-full w-48 text-md text-center p-2 m-1 uppercase"
          />
          <label class="mt-4">ends with...</label>
          <input
            v-on:change="findWords()"
            v-model="ends"
            placeholder=""
            class="rounded-full w-48 text-md text-center p-2 m-1 uppercase"
          />
        </div>
        <div class="flex flex-col mx-auto sm:mr-auto sm:ml-4 md:ml-8">
          <label class="mt-4">contains...</label>
          <input
            v-on:change="findWords()"
            v-model="contains"
            placeholder=""
            class="rounded-full w-48 text-md text-center p-2 m-1 uppercase"
          />
          <label class="mt-4">it's length...</label>
          <input
            v-on:change="findWords()"
            type="number"
            v-model.number="length"
            placeholder=""
            class="rounded-full w-48 text-md text-center p-2 m-1 uppercase"
          />
        </div>
      </div>
      <button
        v-on:click="findWords()"
        class="
          w-9/12
          sm:w-7/12
          md:w-5/12
          lg:w-80
          mx-auto
          bg-white
          p-2
          m-10
          rounded-full
        "
      >
        SEARCH
      </button>
    </div>

    <loading
      class="mx-auto"
      v-bind:active="isLoading"
      :can-cancel="true"
      :on-cancel="onCancel"
      :is-full-page="true"
    />
    <div class="mb-10 p-0" v-if="words !== {} && !justLoaded">
      <ul>
        <li
          class="m-1 py-1 px-2 bg-gray-800 rounded-lg text-white inline-block"
          v-for="(w, key) in words"
          v-bind:key="key"
        >
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
    <p class="m-10 text-gray-800" v-if="!words.length && !justLoaded">
      No words were found.
    </p>

    <CommonFooter />
  </div>
</template>

<script>
import axios from "axios";
import CommonFooter from "../components/CommonFooter.vue";
import loading from "vue-loading-overlay";

export default {
  name: "Home",
  props: {
    msg: String,
  },
  components: {
    CommonFooter,
    loading,
  },
  data() {
    return {
      starts: "",
      ends: "",
      contains: "",
      length: 0,
      words: {},
      justLoaded: true,
      isLoading: false,
    };
  },
  computed: {
    "uppercase-letters": function () {
      return this.letters.toUppercase();
    },

    noData: function () {
      if (this.justLoaded) return true;
      return !this.words.length;
    },
  },

  mounted: function () {},

  methods: {
    findWords() {
      this.justLoaded = false;
      // console.log(this.starts, this.contains, this.ends, this.length);
      const searchWord = this.starts + "*" + this.contains + "*" + this.ends;

      this.showLoadingSpin();
      axios
        .get(`https://api.datamuse.com/words?sp=${searchWord}`)
        .then((response) => (this.words = response.data))
        .then(() => {
          this.onCancel();
          if (this.length)
            return (this.words = this.words.filter(
              (item) => item.word.length === this.length
            ));
          else {
            return this.words;
          }
        });
    },

    showLoadingSpin() {
      this.isLoading = !this.isLoading;
      // console.log(this.isLoading);
    },

    onCancel() {
      this.isLoading = false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@media only screen and (min-width: 10px) {
  .home {
    background-color: #42b983;
    font-family: "Source Sans Pro", sans-serif;
  }

  .content {
    font-family: "Source Sans Pro", sans-serif;
  }
}
</style>
