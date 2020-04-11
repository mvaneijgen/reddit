<template>
  <div class="component-RenameMe">
    <h1>reddit-dashboard</h1>
    <ul>
      <!-- <post v-for="(item, index) in getPosts.data.children" :key="index" :item="item"></post> -->
    </ul>
    <!-- <pre>{{getPosts.data.children}}</pre> -->
  </div>
</template>

<script>
// import { mapGetters } from "vuex";
import post from "@/components/reddit/post.vue";

export default {
  // props: ['item'],

  name: "RenameMe",
  data() {
    return {
      title: "RenameMe",
      data: {},
    };
  }, // End data
  components: {
    post,
  },
  computed: {
    // ...mapGetters({
    //   getData: "posts/getPosts",
    // }),
    getData: state => id => {
      return state.todos.find(todo => todo.id === id);
    },
  }, // Data with computed logic
  methods: {
    //   // async fetchSomething() {
    //   //   const data = await this.$axios.$get(`r/vuejs/new.json`);
    //   //   this.data = data.data.children;
    //   // },
    //       async asyncData({ query, error }) {
    //     const data = await this.$axios.$get(`r/vuejs/new.json`);
    //     this.data = data.data.children;
    //   },
    //   export default {
    // async asyncData({ query, error }) {
    //   let [pageRes, countRes] = await Promise.all([
    //     axios.get('/api/post/page/0'),
    //     axios.get('/api/post/count/published'),
    //   ])
    //   return {
    //      posts: pageRes.data.list,
    //      total: countRes.data.result
    //   }
    // }
  },
  // watch: {}, // Watchs data, needs to have the same name as the data that is being watched

  // // Lifecycle hook. Check for more https://vuejs.org/v2/guide/instance.html or https://vuejs.org/v2/api/#Options-Lifecycle-Hooks
  // beforeCreate() {},
  created() {
    // this.fetchSomething();
  }, // Each time the app is created (once?)
  // beforeMount() {},
  // mounted() {}, // Be sure all elements are drawn. Here you can use normal Javascript to interact with your page
  // beforeUpdate() {},
  // update() {},
  // activated() {},
  // deactivated() {},
  // beforeDestroy() {},
  // destroyed() {},
  // errorCaptured() {},
};
</script>