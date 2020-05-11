<template>
  <li class="component-post" :data-sub="item.data.subreddit" :class="{ external: !item.data.selftext_html }">
    <div class="content">
      <div class="base">
        <div class="inner">
          <template v-if="!item.data.selftext_html">
            <div class="small" v-if="item.data.ups > 1 && !item.data.title ||item.data.ups > 30 || item.data.author === 'mvaneijgen'">🔺{{item.data.ups}}</div>
          </template>
          <h3 v-if="item.data.title" class="title"><a :href="'//reddit.com'+item.data.permalink" target="_blank">{{item.data.title}}</a></h3>
          <h3 v-else class="title"><small>➡</small> <a :href="'//reddit.com'+item.data.permalink" target="_blank">{{item.data.link_title}}</a></h3>
          <template v-if="!item.data.selftext_html">
            <div class="small" v-if="item.data.ups < 2">💬 {{item.data.num_comments}}</div>
          </template>
        </div>
        <template v-if="!item.data.selftext_html">
          <div class="label">{{item.data.subreddit}}</div>
        </template>
      </div>

      <ul class="meta" v-if="item.data.selftext_html" @click="clickToggle">
        <ul>
          <li v-if="item.data.ups > 1 && !item.data.title ||item.data.ups > 30 || item.data.author === 'mvaneijgen'">🔺{{item.data.ups}}</li>
          <li v-if="item.data.ups < 2">💬 {{item.data.num_comments}}</li>
          <li>u/{{item.data.author}}</li>
        </ul>
        <ul>
          <li><time>{{$moment.unix(item.data.created_utc).fromNow()}}</time></li>
          <li class="label">{{item.data.subreddit}}</li>
        </ul>
      </ul>
      <div v-if="toggle" v-html="decodeHTML(item.data.selftext_html)" class="text"></div>
      <div v-if="item.data.author === 'mvaneijgen'" v-html="decodeHTML(item.data.body_html)" class="text"></div>
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
  methods: {
    clickToggle() {
      this.toggle = !this.toggle;
    },
    decodeHTML(html) {
      const txt = document.createElement("textarea");
      txt.innerHTML = html;
      return txt.value;
    },
  }, // Are functions run on user actions example @click or on lifecycle hooks
};
</script>
