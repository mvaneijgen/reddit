<template>
  <div class="component-getSubs">
    <ul>
      <post v-for="(item, index) in sortPosts" :key="index" :item="item"></post>
    </ul>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import post from "@/components/reddit/post.vue";

export default {
  props: ["subs"],
  name: "getSubs",
  data() {
    return {
      posts: [],
    };
  }, // End data
  components: {
    post,
  },
  computed: {
    getSubs() {
      return this.$store.getters["reddit/getSubs"](this.subs);
    },
    getPosts() {
      return this.$store.getters["reddit/getPosts"](this.subs);
    },
    sortPosts() {
      const posts = this.getPosts;
      return [...posts].sort((a, b) => b.data.created - a.data.created);
      // .slice(0, 50);
    },
  }, // Data with computed logic
  methods: {
    async asyncSubPosts(sub) {
      let path = `r/${sub}/new.json?limit=7`;
      if (sub === "user/mvaneijgen") {
        path = `${sub}.json?limit=20`;
      }

      // this.$axios.setHeader("Access-Control-Allow-Origin", "*");
      const data = await this.$axios.$get(path);
      const payload = {
        sub: this.subs,
        posts: data.data.children,
      };
      this.$store.commit("reddit/addPosts", payload);
    },
    async fetchSubPosts(sub) {
      let path = `r/${sub}/new.json?limit=7`;
      if (sub === "user/mvaneijgen") {
        path = `${sub}.json?limit=20`;
      }

      const baseURL = "https://www.reddit.com/";
      let url = `${baseURL}${path}`;

      const data = await fetch(url)
        .then(response => {
          return response.json();
        })
        .then(data => {
          console.log(data);
          const payload = {
            sub: this.subs,
            posts: data.data.children,
          };
          this.$store.commit("reddit/addPosts", payload);
        });
    },
  },
  mounted() {
    this.getSubs.forEach(sub => {
      if (this.getPosts.length === 0) {
        this.fetchSubPosts(sub);
      }
    });
  },
  created() {}, // Each time the app is created (once?)
};
</script>