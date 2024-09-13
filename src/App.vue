<template>
  <!-- ARTICLE -->
  <div class="container mt-5">
    <div class="col-md-6 col">
      <input class="form-control" type="search" placeholder="Search" v-model="search" />
      <small v-if="filteredResults.length">
        {{ filteredResults.length }} Posts were found.
      </small>
    </div>

    <div class="row mt-5">
      <div class="col-sm-12" v-for="d in data" :key="d">
        <h2 v-html="highlight(d.title)"></h2>
        <h5 class="text-muted" v-html="highlight(d.date)"></h5>
        <p v-html="highlight(d.description)"></p>
        <hr />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: "",
      count: 0,
      data: [
        {
          title: "JavaScript Tutorial",
          date: "Created on 10/10/2023",
          description:
            "JavaScript is the world's most popular programming language. JavaScript is the programming language of the Web.JavaScript is easy to learn.This tutorial will teach you JavaScript from basic to advanced.",
        },
        {
          title: "Python Tutorial",
          date: "Created on 10/10/2023",
          description:
            "Python is a popular programming language. Python can be used on a server to create web applications.",
        },
        {
          title: "PHP Tutorial",
          date: "Created on 10/10/2023",
          description:
            "PHP is a server scripting language, and a powerful tool for making dynamic and interactive Web pages.PHP is a widely-used, free, and efficient alternative to competitors such as Microsoft's ASP.",
        },
      ],
    };
  },
  computed: {
    filteredResults() {
      const pattern = new RegExp(this.search, "gi");

      const filteredPosts = this.data.filter((post) => {
        return (
          post.title.match(pattern) ||
          post.description.match(pattern) ||
          post.date.match(pattern)
        );
      });

      return filteredPosts;
    },
  },
  methods: {
    highlight(data = "") {
      if (this.search) {
        const pattern = new RegExp(this.search, "gi");
        const highlightedData = data.replace(
          pattern,
          `<span class="hl-search">${this.search}</span>`
        );
        return highlightedData;
      }
      return data;
    },
  },
};
</script>

<style>
.hl-search {
  background-color: yellow;
}
</style>
