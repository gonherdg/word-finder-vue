<template>
  <div
    class="
      home
      flex flex-col
      bg-gradient-to-r
      from-green-400
      via-green-200
      to-blue-100
    "
  >
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
    <div class="mb-10 p-0 bg-transparent" v-if="words !== {} && !justLoaded">
      <ul class="bg-transparent">
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
    background-color: #79d9a7;
    background-color: #b8ffd5;
background-color: #b8ffd5;
background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 2000 1500'%3E%3Cdefs%3E%3Crect stroke='%23b8ffd5' stroke-width='.5' width='1' height='1' id='s'/%3E%3Cpattern id='a' width='3' height='3' patternUnits='userSpaceOnUse' patternTransform='scale(50) translate(-980 -735)'%3E%3Cuse fill='%23b4fad1' href='%23s' y='2'/%3E%3Cuse fill='%23b4fad1' href='%23s' x='1' y='2'/%3E%3Cuse fill='%23b1f5cc' href='%23s' x='2' y='2'/%3E%3Cuse fill='%23b1f5cc' href='%23s'/%3E%3Cuse fill='%23adf0c8' href='%23s' x='2'/%3E%3Cuse fill='%23adf0c8' href='%23s' x='1' y='1'/%3E%3C/pattern%3E%3Cpattern id='b' width='7' height='11' patternUnits='userSpaceOnUse' patternTransform='scale(50) translate(-980 -735)'%3E%3Cg fill='%23a9ebc4'%3E%3Cuse href='%23s'/%3E%3Cuse href='%23s' y='5' /%3E%3Cuse href='%23s' x='1' y='10'/%3E%3Cuse href='%23s' x='2' y='1'/%3E%3Cuse href='%23s' x='2' y='4'/%3E%3Cuse href='%23s' x='3' y='8'/%3E%3Cuse href='%23s' x='4' y='3'/%3E%3Cuse href='%23s' x='4' y='7'/%3E%3Cuse href='%23s' x='5' y='2'/%3E%3Cuse href='%23s' x='5' y='6'/%3E%3Cuse href='%23s' x='6' y='9'/%3E%3C/g%3E%3C/pattern%3E%3Cpattern id='h' width='5' height='13' patternUnits='userSpaceOnUse' patternTransform='scale(50) translate(-980 -735)'%3E%3Cg fill='%23a9ebc4'%3E%3Cuse href='%23s' y='5'/%3E%3Cuse href='%23s' y='8'/%3E%3Cuse href='%23s' x='1' y='1'/%3E%3Cuse href='%23s' x='1' y='9'/%3E%3Cuse href='%23s' x='1' y='12'/%3E%3Cuse href='%23s' x='2'/%3E%3Cuse href='%23s' x='2' y='4'/%3E%3Cuse href='%23s' x='3' y='2'/%3E%3Cuse href='%23s' x='3' y='6'/%3E%3Cuse href='%23s' x='3' y='11'/%3E%3Cuse href='%23s' x='4' y='3'/%3E%3Cuse href='%23s' x='4' y='7'/%3E%3Cuse href='%23s' x='4' y='10'/%3E%3C/g%3E%3C/pattern%3E%3Cpattern id='c' width='17' height='13' patternUnits='userSpaceOnUse' patternTransform='scale(50) translate(-980 -735)'%3E%3Cg fill='%23a6e5c0'%3E%3Cuse href='%23s' y='11'/%3E%3Cuse href='%23s' x='2' y='9'/%3E%3Cuse href='%23s' x='5' y='12'/%3E%3Cuse href='%23s' x='9' y='4'/%3E%3Cuse href='%23s' x='12' y='1'/%3E%3Cuse href='%23s' x='16' y='6'/%3E%3C/g%3E%3C/pattern%3E%3Cpattern id='d' width='19' height='17' patternUnits='userSpaceOnUse' patternTransform='scale(50) translate(-980 -735)'%3E%3Cg fill='%23b8ffd5'%3E%3Cuse href='%23s' y='9'/%3E%3Cuse href='%23s' x='16' y='5'/%3E%3Cuse href='%23s' x='14' y='2'/%3E%3Cuse href='%23s' x='11' y='11'/%3E%3Cuse href='%23s' x='6' y='14'/%3E%3C/g%3E%3Cg fill='%23a2e0bb'%3E%3Cuse href='%23s' x='3' y='13'/%3E%3Cuse href='%23s' x='9' y='7'/%3E%3Cuse href='%23s' x='13' y='10'/%3E%3Cuse href='%23s' x='15' y='4'/%3E%3Cuse href='%23s' x='18' y='1'/%3E%3C/g%3E%3C/pattern%3E%3Cpattern id='e' width='47' height='53' patternUnits='userSpaceOnUse' patternTransform='scale(50) translate(-980 -735)'%3E%3Cg fill='%2391ffbe'%3E%3Cuse href='%23s' x='2' y='5'/%3E%3Cuse href='%23s' x='16' y='38'/%3E%3Cuse href='%23s' x='46' y='42'/%3E%3Cuse href='%23s' x='29' y='20'/%3E%3C/g%3E%3C/pattern%3E%3Cpattern id='f' width='59' height='71' patternUnits='userSpaceOnUse' patternTransform='scale(50) translate(-980 -735)'%3E%3Cg fill='%2391ffbe'%3E%3Cuse href='%23s' x='33' y='13'/%3E%3Cuse href='%23s' x='27' y='54'/%3E%3Cuse href='%23s' x='55' y='55'/%3E%3C/g%3E%3C/pattern%3E%3Cpattern id='g' width='139' height='97' patternUnits='userSpaceOnUse' patternTransform='scale(50) translate(-980 -735)'%3E%3Cg fill='%2391ffbe'%3E%3Cuse href='%23s' x='11' y='8'/%3E%3Cuse href='%23s' x='51' y='13'/%3E%3Cuse href='%23s' x='17' y='73'/%3E%3Cuse href='%23s' x='99' y='57'/%3E%3C/g%3E%3C/pattern%3E%3C/defs%3E%3Crect fill='url(%23a)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23b)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23h)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23c)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23d)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23e)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23f)' width='100%25' height='100%25'/%3E%3Crect fill='url(%23g)' width='100%25' height='100%25'/%3E%3C/svg%3E");
background-attachment: local;
background-size: auto;
  }

  .content {
    font-family: "Source Sans Pro", sans-serif;
  }
}
</style>
