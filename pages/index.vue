<template>
  <div class="block">
    <SearchJoke v-on:search-text="searchText" :numbers="totalItems" />
    <el-container v-loading="loading">
      <el-main>
        <el-pagination
          :page-size="20"
          layout="prev, pager, next"
          :total="totalItems"
          :current-page.sync="currentPage"
          v-on:current-change="changePage"
        />
        <Joke
          v-for="joke in jokes"
          :key="joke.id"
          :id="joke.id"
          :joke="joke.joke"
          :query="textSearch"
        />
      </el-main>
    </el-container>
  </div>
</template>

<script>
import axios from "axios";
import Joke from "../components/Joke";
import SearchJoke from "../components/SearchJoke";

export default {
  components: {
    SearchJoke,
    Joke
  },
  data() {
    return {
      totalItems: 0,
      currentPage: 1,
      textSearch: "",
      loading: false,
      jokes: []
    };
  },
  async created() {
    this.fetchJoke(this.textSearch, this.currentPage);
  },
  methods: {
    async fetchJoke(text, page) {
      const config = {
        headers: {
          Accept: "application/json"
        }
      };
      try {
        this.loading = true;
        const res = await axios.get(
          `https://icanhazdadjoke.com/search?term=${text}&page=${this.currentPage}`,
          config
        );
        this.loading = false;
        this.jokes = res.data.results;
        this.totalItems = res.data.total_jokes;
      } catch (err) {
        this.$notify.error({
          title: "Error",
          message: err.message
        });
      }
    },
    searchText(text) {
      this.textSearch = text;
      this.currentPage = 1;
      this.fetchJoke(this.textSearch, this.currentPage);
    },
    changePage() {
      this.fetchJoke(this.textSearch, this.currentPage);
    }
  },
  head() {
    return {
      title: "hello"
    };
  }
};
</script>

<style></style>
