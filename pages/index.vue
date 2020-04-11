<template>
  <main>
    <getSubs subs="subsMain" />
    <getSubs subs="subsOther" />
    <getSubs subs="subsSmall" />
    <getSubs subs="personal" />
  </main>
</template>

<script>
import getSubs from "@/components/reddit/getSubs.vue";

export default {
  data() {
    return {};
  },
  components: {
    getSubs,
  },
};
</script>
