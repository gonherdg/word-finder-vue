<template>
  <div class="background">
    <div class="main">
      <div class="flex-parent">
        <div class="subtitle">About the app:</div>

        <div>
          <p>
            This was made using Vue.js and CSS on the front-end. I'm also using
            Datamuse API to obtain all the words that matches the input.
          </p>

          <p>
            Finally, you can click on any word and you will be redirected to the
            definition of this word at dictionary.com.
          </p>

          <p>The job is part of my training as a front-end developer.</p>
        </div>
      </div>

      <div class="flex-parent">
        <div class="subtitle">About me:</div>

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

      <div class="flex-parent">
        <div class="subtitle">Contact me:</div>

        <div>
          <p>
            Have an interesting app in mind to work on? Want to see more of my
            work?
          </p>

          <p>
            Contact me at <a href="http://gonsoft.com.ar">www.gonsoft.com.ar</a>
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
<style scoped>
.background {
  background-color: white;
}

.main {
  max-width: 60%;
  margin: auto;
  margin-top: 1rem;
  margin-bottom: 1rem;
  padding: 2rem;
  background-color: #eee;
  text-align: justify;
}

.flex-parent {
  display: flex;
  flex-direction: column;
  padding-bottom: 1rem;
}

.subtitle {
  padding-left: 1rem;
  padding-right: 1rem;
  font-style: italic;
  font-size: large;
  color: #222;
  padding: 0.5rem;
}

p {
  padding: 0rem;
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
