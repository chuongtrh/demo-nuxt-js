<template>
  <div class="searchJoke">
    <el-form :inline="true">
      <el-form-item>
        <el-input v-model="text" placeholder="Search jokes"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" icon="el-icon-search" @click="onSubmit"
          >Search</el-button
        >
      </el-form-item>
      <span
        ><b>{{ numbers }}</b> jokes found</span
      >
    </el-form>
  </div>
</template>

<script>
export default {
  name: "SearchJokes",
  props: {
    numbers: {
      type: Number,
      required: true,
      default: 0
    }
  },
  data() {
    return {
      componentKey: 0,
      text: ""
    };
  },
  methods: {
    onSubmit() {
      this.$emit("search-text", this.text);
    }
  }
};
</script>

<style>
.searchJoke {
  padding: 0 1rem;
  margin: 1rem 0 0 0;
}
</style>
