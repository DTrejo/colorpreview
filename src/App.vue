<template>
<div id="app">
    <!-- <img width="25%" src="./assets/logo.png"> -->
    <!-- <HelloWorld/> -->
    <!--<pre>
      {{JSON.stringify(combos, null, 2)}}
    </pre>
    -->
    <textarea
      placeholder="Paste your full hex colors here"
      v-model="hexes"
    />
    <!-- <input 
      type="color"
      v-for="hex in hexesClean"
      :value="hex"
    /> -->
    <section 
      v-for="c in combos" :key="c.hex"
      :style="{backgroundColor: c.hex}"
    >
      <p 
        style="text-align:right; color: rgba(0,0,0,.5)"
      >
        background-color: {{c.hex}}
      </p>
      <template 
        v-for="(c2, i) in c.combinations"
        :style="{color: c2.hex}"
      >
        <h1
          :key="heading(i) + c2.hex"
          :is="heading(i)"
          :style="{color: c2.hex}"
        >
          {{heading(i)}} color: {{c2.hex}}
        </h1>
        <p
          :key="'p' + c2.hex"
          :style="{color: c2.hex}"
        >
          Lorem, ipsum dolor sit amet consectetur
          <span style="text-decoration: underline">adipisicing elit</span>. 
          Praesentium consequuntur quo, maiores in velit iusto
          <strong>excepturi assumenda autem odio</strong>,
          maxime perspiciatis dolorem asperiores hic enim nisi adipisci,
          <em>possimus ratione earum</em>!
        </p> 
      </template>
    </section>
</div>
</template>

<script>
// import HelloWorld from './components/HelloWorld'
import colorable from "colorable";

const headings = ["h1", "h2", "h3", "h4", "h5", "h6"];

export default {
  name: "App",
  computed: {
    hexesClean: function() {
      return this.hexes
        .split(" ")
        .map(s => s.trim())
        .filter(s => s);
    },
    combos: function() {
      // debugger
      return colorable(this.hexesClean, {
        compact: true,
        threshold: 3
      });
    }
  },
  data: function() {
    return {
      // #cc7d81 #d78784 #ea9268 #eebf55 #c1dede #eeda92 #e7dec3 #f0eecd #835267 #4998c6
      // hexes: "#010003 #010e1f #072738 #013b46 #025656 #02806e #8d8a6a #0293d7",
      hexes: "#f0eecd #e7dec3 #d0be7f #90a6a6 #ae8b3c #a7633f #833b37 #522427"
        .split(" ")
        .reverse()
        .join(" ")
    };
  },
  methods: {
    heading(index) {
      return headings[index] || headings[headings.length - 1];
    }
  },
  components: {
    // HelloWorld
  }
};
</script>

<style lang="stylus">
body, *
  margin 0

* + * 
  margin-top 1.5em

#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  color #222

textarea
  display block
  font-size 1rem
  width calc(100% - 2rem)
  padding 1em
  margin-bottom 0
  box-shadow: inset 0 0 1rem rgba(0, 0, 0, .5)
  border-radius 0

section
  margin-top 0
  padding-top 1.5em
  padding-bottom 5em

  p, h1, h2, h3, h4, h5, h6, div
    max-width 33rem
    margin-left auto
    margin-right auto
    padding-left 1rem
    padding-right 1rem

</style>
