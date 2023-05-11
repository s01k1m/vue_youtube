<template>
  <div id="app">
    <h1>SSAFY TUBE</h1>
    <TheSearchBar @search="doSearch"></TheSearchBar>
    <div v-if="videoUrl">
      <iframe id="ytplayer" type="text/html" :src="`${videoUrl}`" width="720" height="405" frameborder="0" allowfullscreen></iframe>
      <!-- 스니펫으로 가져왔따면 이름이 있었을 것이다. 다만 나ㅡㄴㄴ 아이디라 없으니패스
       -->
    </div>
        <!-- <div>{{ video.items[0].id.videoId }}</div> -->
    <div>{{ videoUrl }}</div>
  </div>
</template>

<script>
import TheSearchBar from './components/TheSearchBar.vue'
import axios from 'axios';

export default {
  name: 'App',
  components: {
    TheSearchBar
  },
  data() {
    return {
      video : {
        "kind": "youtube#searchListResponse",
        "etag": "K6DNDp57cLmXNvoesoSxWNbrl20",
        "nextPageToken": "CAEQAA",
        "regionCode": "KR",
        "pageInfo": {
            "totalResults": 925021,
            "resultsPerPage": 1
        },
        "items": [
            {
                "kind": "youtube#searchResult",
                "etag": "SHnCOVNhpqE-kzDjW9q1QnHf_9o",
                "id": {
                    "kind": "youtube#video",
                    "videoId": "5bOFSroc274"
                }
            }
        ]
    },
    imgUrl : '', // 초기화
    value : ''
  }
  },
  computed: {
    videoUrl : function() {
      // 초기값을 주고 default 가 있다.
      return 'https://www.youtube.com/embed/'+this.video.items[0]?.id.videoId
    }
  },
  methods: {
    doSearch(n) {
      this.value = n
    //   },
    // fetchData: function() {
      axios.get(`https://www.googleapis.com/youtube/v3/search?part=id&q=${this.value}&maxResults=1&key=${process.env.VUE_APP_YOUTUBE_API_KEY}`)
      .then((response) => {
        console.log(response)
        // cess-Control-Allow-Origin' error
        this.video = response.data
      })
      .catch((error) => {
        console.log(error)
      })
    }
    }
    //created hook 을 이용하여 App.vue 가 렌더링 될 때, youtube api 를 활용 해 AJAX 요청을 보냅니다. 이때, 검색어는 코딩노래 입니다
  // 응답 받은 데이터의 첫 번째 비디오를 화면에 출력냅니다. 

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
