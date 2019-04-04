<template>
  <div>
    <ul>
      <li v-for="(item, index) in list" :key="index">
        {{ item.snippet.title }} <a :href="`https://youtube.com/c/${item.snippet.channelId}`" target="_blank">링크</a>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'callback',
  data () {
    return {
      params: {},
      list: []
    }
  },
  mounted () {
    location.hash.replace('#', '').split('&').forEach(item => {
      const value = item.split('=')
      this.params[value[0]] = value[1]
    })
    this.loadData()
  },
  methods: {
    async loadData (pageToken = '') {
      const params = {
        part: 'snippet',
        mine: 'true'
      }
      if (pageToken) {
        params.pageToken = pageToken
      } else {
        this.list = []
      }
      const url = 'https://www.googleapis.com/youtube/v3/subscriptions?part=snippet&mine=true'
      const { data } = await axios.get(url, {
        headers: {
          Authorization: 'Bearer ' + this.params['access_token']
        },
        params
      })
      data.items.forEach(item => this.list.push(item))
      if (data.nextPageToken) {
        this.loadData(data.nextPageToken)
      }
    }
  }
}
</script>
