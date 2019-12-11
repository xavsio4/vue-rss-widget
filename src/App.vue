<template>
  <div id="app">
    <rss-widget feed="https://api.rss2json.com/v1/api.json?rss_url=https%3A%2F%2Ftechcrunch.com%2Ffeed%2F">
      
      <template v-slot:feed_header="slotProps">
        <h2>{{slotProps.rssfeed.title}}</h2>
      </template>

      <template v-slot:feed_body="slotProps">
        <ul >
          <li v-for="(item,i) in slotProps.items" :key="i">
            <div class="card">
              <div class="card-header">
                  <h4>{{item.title}}</h4>
              </div>
              <div class="card-body">
                  {{item.description}}
              </div>
            </div>
          </li>
        </ul>
      </template>
    </rss-widget>
  </div>
</template>

<script>
import RssWidget from './components/RssWidget.vue'

export default {
  name: 'app',
  components: {
    RssWidget
  }
}
</script>

<style>

</style>
