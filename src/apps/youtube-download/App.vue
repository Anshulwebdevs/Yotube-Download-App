<template>
  <div class="container">
    <span class="text-center"><h3>Youtube Download</h3></span>
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row">
    <VideoLinksTable :info="info"></VideoLinksTable>
    <VideoList :data="videos" @videoSelect="onVideoSelect" @navigation="onNavigation"></VideoList>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from '../../components/SearchBar';
import VideoList from '../../components/VideoList';
import VideoLinksTable from '../../components/VideoLinksTable';
const API_KEY = 'AIzaSyAHuTTiQul72c39CW6z1h3nhvdEgVlCdiw';

export default {
  
  name: 'YoutubeDownloader',
  components: {
    SearchBar,
    VideoList,
    VideoLinksTable
  },
  data(){
    return {
      videos:[],
      info:null,
      nav:null,
      searchTerm:''
    }
  },
  methods:{
    onVideoSelect(video){
      axios.get('http://www.anshul.cf/dl/',{
        params:{
          video_id:video.id.videoId
        }
      }).then(res => {
        // console.log(video);
        this.info = {data:res.data, video};
      });
    },
    onTermChange(searchTerm){
       if(searchTerm === '') {
        this.videos = [];
        return;
       }
       this.searchTerm = searchTerm;
      axios.get('https://www.googleapis.com/youtube/v3/search',{
        params:{
          key: API_KEY,
          type:'video',
          part:'snippet',
          videoDefinition:'standard',
          q:searchTerm
        }
      }).then(response => {
        // console.log(response.data);
        this.videos = response.data;
        // let next = response.data.nextPageToken || '';
        // let prev = response.data.prevPageToken || '';
        // this.nav = {next, prev};
        // this.selectedVideo = this.videos.items[0];
      });
    },
    onNavigation(pageToken){
      // console.log(pageToken,"page token");
      axios.get('https://www.googleapis.com/youtube/v3/search',{
        params:{
          key: API_KEY,
          type:'video',
          part:'snippet',
          videoDefinition:'standard',
          q:this.searchTerm,
          pageToken:pageToken
        }
      }).then(response => {
        this.videos = response.data;

      });
    }

  }
}
</script>

<style>
body{
  margin-top: 20px; 
}
</style>
