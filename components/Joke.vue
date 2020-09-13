<template>
  <div class="joke">
    <p v-html="highlight()"></p>
  </div>
</template>

<script>
export default {
  name: "Joke",
  props: ["joke", "id", "query"],
  methods: {
    highlight() {
      if (!this.query) {
        return this.joke;
      }
      return this.joke.replace(new RegExp(this.query, "gi"), match => {
        return '<span class="highlightText">' + match + "</span>";
      });
    }
  }
};
</script>

<style>
.joke {
  padding: 1rem;
  border: 1px dotted #ccc;
  margin: 1rem 0;
}

.highlightText {
  background: yellow;
}
</style>
