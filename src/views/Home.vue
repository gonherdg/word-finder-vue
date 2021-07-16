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
.home {
  font-family: "Source Sans Pro", sans-serif;
  background-attachment: local;
  background-size: auto;
  background-color: #63dfa4;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='776' height='646.7' viewBox='0 0 1080 900'%3E%3Cg fill-opacity='.1'%3E%3Cpolygon fill='%23444' points='90 150 0 300 180 300'/%3E%3Cpolygon points='90 150 180 0 0 0'/%3E%3Cpolygon fill='%23AAA' points='270 150 360 0 180 0'/%3E%3Cpolygon fill='%23DDD' points='450 150 360 300 540 300'/%3E%3Cpolygon fill='%23999' points='450 150 540 0 360 0'/%3E%3Cpolygon points='630 150 540 300 720 300'/%3E%3Cpolygon fill='%23DDD' points='630 150 720 0 540 0'/%3E%3Cpolygon fill='%23444' points='810 150 720 300 900 300'/%3E%3Cpolygon fill='%23FFF' points='810 150 900 0 720 0'/%3E%3Cpolygon fill='%23DDD' points='990 150 900 300 1080 300'/%3E%3Cpolygon fill='%23444' points='990 150 1080 0 900 0'/%3E%3Cpolygon fill='%23DDD' points='90 450 0 600 180 600'/%3E%3Cpolygon points='90 450 180 300 0 300'/%3E%3Cpolygon fill='%23666' points='270 450 180 600 360 600'/%3E%3Cpolygon fill='%23AAA' points='270 450 360 300 180 300'/%3E%3Cpolygon fill='%23DDD' points='450 450 360 600 540 600'/%3E%3Cpolygon fill='%23999' points='450 450 540 300 360 300'/%3E%3Cpolygon fill='%23999' points='630 450 540 600 720 600'/%3E%3Cpolygon fill='%23FFF' points='630 450 720 300 540 300'/%3E%3Cpolygon points='810 450 720 600 900 600'/%3E%3Cpolygon fill='%23DDD' points='810 450 900 300 720 300'/%3E%3Cpolygon fill='%23AAA' points='990 450 900 600 1080 600'/%3E%3Cpolygon fill='%23444' points='990 450 1080 300 900 300'/%3E%3Cpolygon fill='%23222' points='90 750 0 900 180 900'/%3E%3Cpolygon points='270 750 180 900 360 900'/%3E%3Cpolygon fill='%23DDD' points='270 750 360 600 180 600'/%3E%3Cpolygon points='450 750 540 600 360 600'/%3E%3Cpolygon points='630 750 540 900 720 900'/%3E%3Cpolygon fill='%23444' points='630 750 720 600 540 600'/%3E%3Cpolygon fill='%23AAA' points='810 750 720 900 900 900'/%3E%3Cpolygon fill='%23666' points='810 750 900 600 720 600'/%3E%3Cpolygon fill='%23999' points='990 750 900 900 1080 900'/%3E%3Cpolygon fill='%23999' points='180 0 90 150 270 150'/%3E%3Cpolygon fill='%23444' points='360 0 270 150 450 150'/%3E%3Cpolygon fill='%23FFF' points='540 0 450 150 630 150'/%3E%3Cpolygon points='900 0 810 150 990 150'/%3E%3Cpolygon fill='%23222' points='0 300 -90 450 90 450'/%3E%3Cpolygon fill='%23FFF' points='0 300 90 150 -90 150'/%3E%3Cpolygon fill='%23FFF' points='180 300 90 450 270 450'/%3E%3Cpolygon fill='%23666' points='180 300 270 150 90 150'/%3E%3Cpolygon fill='%23222' points='360 300 270 450 450 450'/%3E%3Cpolygon fill='%23FFF' points='360 300 450 150 270 150'/%3E%3Cpolygon fill='%23444' points='540 300 450 450 630 450'/%3E%3Cpolygon fill='%23222' points='540 300 630 150 450 150'/%3E%3Cpolygon fill='%23AAA' points='720 300 630 450 810 450'/%3E%3Cpolygon fill='%23666' points='720 300 810 150 630 150'/%3E%3Cpolygon fill='%23FFF' points='900 300 810 450 990 450'/%3E%3Cpolygon fill='%23999' points='900 300 990 150 810 150'/%3E%3Cpolygon points='0 600 -90 750 90 750'/%3E%3Cpolygon fill='%23666' points='0 600 90 450 -90 450'/%3E%3Cpolygon fill='%23AAA' points='180 600 90 750 270 750'/%3E%3Cpolygon fill='%23444' points='180 600 270 450 90 450'/%3E%3Cpolygon fill='%23444' points='360 600 270 750 450 750'/%3E%3Cpolygon fill='%23999' points='360 600 450 450 270 450'/%3E%3Cpolygon fill='%23666' points='540 600 630 450 450 450'/%3E%3Cpolygon fill='%23222' points='720 600 630 750 810 750'/%3E%3Cpolygon fill='%23FFF' points='900 600 810 750 990 750'/%3E%3Cpolygon fill='%23222' points='900 600 990 450 810 450'/%3E%3Cpolygon fill='%23DDD' points='0 900 90 750 -90 750'/%3E%3Cpolygon fill='%23444' points='180 900 270 750 90 750'/%3E%3Cpolygon fill='%23FFF' points='360 900 450 750 270 750'/%3E%3Cpolygon fill='%23AAA' points='540 900 630 750 450 750'/%3E%3Cpolygon fill='%23FFF' points='720 900 810 750 630 750'/%3E%3Cpolygon fill='%23222' points='900 900 990 750 810 750'/%3E%3Cpolygon fill='%23222' points='1080 300 990 450 1170 450'/%3E%3Cpolygon fill='%23FFF' points='1080 300 1170 150 990 150'/%3E%3Cpolygon points='1080 600 990 750 1170 750'/%3E%3Cpolygon fill='%23666' points='1080 600 1170 450 990 450'/%3E%3Cpolygon fill='%23DDD' points='1080 900 1170 750 990 750'/%3E%3C/g%3E%3C/svg%3E");
}

.content {
  font-family: "Source Sans Pro", sans-serif;
}
</style>
