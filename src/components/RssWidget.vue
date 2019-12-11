<template>
  <div class="feed">
    <slot name="feed_header" v-bind:rssfeed="rssfeed">
      <h3>{{ rssfeed.title }}</h3>
      <p>{{ rssfeed.description }}</p>
    </slot>

    <slot name="feed_body" v-bind:items="items">
      <div v-for="(item, i) in items" :key="i" class="card">
        <div class="row">
          <div class="col-md-4">
            <img :src="item.thumbnail" class="w-100" />
          </div>
          <div class="col-md-8 px-3">
            <div class="card-block px-3">
              <h4 class="card-title">{{ item.title }}</h4>
              <p class="card-text">{{ item.description }}</p>
              <a :href="item.link">Read More</a>
            </div>
            <div class="pull-left">
              Author: {{ item.author }} | published on: {{ item.pubDate }}
            </div>
            <div>
              <span
                v-for="(cat, x) in item.categories"
                :key="x"
                class="badge badge-blue"
                >{{ cat }}</span
              >
            </div>
          </div>
        </div>
      </div>
    </slot>
  </div>
</template>

<script>
//not being used yet :>
// nicer, I think, list
/*let colors = [
  "indigo",
  "blue",
  "cyan",
  "light-blue",
  "teal",
  "light-green",
  "blue-grey"
];*/

export default {
  name: "rssfeed",
  props: {
    feed: {
      type: String,
      default:
        "https://api.rss2json.com/v1/api.json?rss_url=https%3A%2F%2Ftechcrunch.com%2Ffeed%2F"
    },
    title_widget: {
      type: String,
      default: ""
    }
  },
  data() {
    return {
      // result: [],
      rssfeed: { title: "", url: "", link: "", description: "", image: "" },
      items: [],
      loading: false
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      this.loading = true;
      const response = await fetch(this.feed);
      const result = await response.json();
      setTimeout(function() {}, 3000);
      this.rssfeed.title = result.feed.title;
      this.rssfeed.description = result.feed.description;
      this.rssfeed.image = result.feed.image;
      this.rssfeed.url = result.feed.url;
      this.items = result.items;
      this.loading = false;
    }
  }
};
</script>

<style scoped>
</style>
