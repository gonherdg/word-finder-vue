<template>
  <div class="bg-white">
    <div
      class="
        w-full
        sm:w-4/5
        md:w-3/4
        lg:w-2/3
        text-sm
        sm:text-base
        mx-auto
        mt-3
        p-8
        bg-gray-200
        text-justify
        min-h-screen
      "
    >
      <div class="flex flex-col pb-4">
        <div class="p-1 italic text-lg text-gray-800">About the app:</div>
        <div>
          <p>
            This was made using Vue.js and Tailwind on the front-end. I'm also using
            Datamuse API to get all the words that matches the input.
          </p>

          <p>
            Finally, you can click on any word and you will be redirected to the
            definition of this word at dictionary.com.
          </p>

          <p>The job is part of my training as a front-end developer.</p>
        </div>
      </div>

      <div class="flex flex-col pb-4">
        <div class="p-1 italic text-lg text-gray-800">About me:</div>

        <div>
          <p>Hello! I'm Gonzalo Del Gaudio, the maker of this app.</p>

          <p>
            I started as a full-stack developer in 2020 looking for a change
            (and on an effort to get the best out of this last year) and excited
            about learning all these new tecnologies (Javascript, Vue, React,
            Node, Express, MongoDB, etc.) to make great web applications.
          </p>

          <p>
            Previously I worked in videogames since 2012, which gave me lots of
            understanding on physics and animation in 2D and 3D as well as other
            languages like C# (Unity), C++ and Python 3.
          </p>
        </div>
      </div>

      <div class="flex flex-col pb-4">
        <div class="p-1 italic text-lg text-gray-800">Contact me:</div>

        <div>
          <p>
            Have an interesting app in mind to work on? Want to see more of my
            work?
          </p>

          <p>
            Contact me at
            <a
              class="text-green-600 hover:text-green-500"
              href="http://gonsoft.com.ar"
              >www.gonsoft.com.ar</a
            >
          </p>
        </div>
      </div>
    </div>
    <CommonFooter />
  </div>
</template>

<script>
import CommonFooter from "../components/CommonFooter.vue";

export default {
  name: "About",
  props: {
    msg: String,
  },
  components: {
    CommonFooter,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
