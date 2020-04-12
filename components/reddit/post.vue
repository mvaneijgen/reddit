<template>
  <li class="component-post" :data-sub="item.data.subreddit">
    <div class="content">
      <h3 v-if="item.data.title" class="title"><a :href="'//reddit.com'+item.data.permalink" target="_blank">{{item.data.title}}</a></h3>
      <h3 v-else class="title"><small>➡</small> <a :href="'//reddit.com'+item.data.permalink" target="_blank">{{item.data.link_title}}</a></h3>
      <button @click="clickToggle">toggle</button>

      <ul class="meta">
        <li v-if="item.data.ups < 2">💬 {{item.data.num_comments}}</li>
        <li v-if="item.data.ups > 1 && !item.data.title ||item.data.ups > 30 || item.data.author === 'mvaneijgen'">🔺 {{item.data.ups}}</li>
        <li><time>{{$moment.unix(item.data.created_utc).fromNow()}}</time></li>
        <li>u/{{item.data.author}}</li>
        <li class="label">{{item.data.subreddit}}</li>
      </ul>
      <div v-if="toggle" v-html="item.data.selftext_html"></div>
      <pre v-if="toggle">{{item.data}}</pre>
    </div>
    <div class="image" v-if="item.data.preview">
      <!-- <img :src="item.data.thumbnail"> -->
      <img :src="item.data.preview.images[0].resolutions[1].url.replace(/amp;/g, '')" alt="test">
      <!-- <img :src="item.data.preview.images[0].resolutions[1].url.replace(/amp;/g, '')" alt="test"> -->
    </div>
  </li>
</template>

<script>
export default {
  props: ["item"],
  name: "post",
  data() {
    return {
      toggle: false,
    };
  }, // End data
  // More info at https://css-tricks.com/methods-computed-and-watchers-in-vue-js/
  // computed: {}, // Data with computed logic
  methods: {
    clickToggle() {
      this.toggle = !this.toggle;
    },
    // format(url) {
    //   return str_replace('amp;', '', url);
    // }
  }, // Are functions run on user actions example @click or on lifecycle hooks
  // watch: {}, // Watchs data, needs to have the same name as the data that is being watched
  // directives: {}, // Create custom v-directives accepts element and bindings

  // // Lifecycle hook. Check for more https://vuejs.org/v2/guide/instance.html or https://vuejs.org/v2/api/#Options-Lifecycle-Hooks
  // beforeCreate() {},
  // created() {}, // Each time the app is created (once?)
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

<style lang="scss" scoped>
// @import '~/assets/css/common/_variables.scss';
</style>