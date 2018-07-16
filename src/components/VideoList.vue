<template>
	<div class="col-md-4">
		<ul class="list-group" v-if="data.items">
			<VideoListItem v-for="video in data.items"
			:video="video"
			:key="video.etag"
			@videoSelect="onVideoSelect"
			></VideoListItem>	
			<li class="list-group-item media">
				<ul class="pagination justify-content-center">
				<li class="page-item"><button class="page-link" v-if="data.prevPageToken" @click="prev">Previous</button></li>
				<li class="page-item"><button class="page-link" v-if="data.nextPageToken" @click="next">Next</button></li>
				</ul>
			</li>
		</ul>
		
	</div>
</template>
<script type="text/javascript">
import VideoListItem from './VideoListItem';
	export default{
		name : 'VideoList',
		props:['data'],
		components:{
			VideoListItem
		},
		methods:{
			onVideoSelect(video){
				this.$emit('videoSelect',video);
			},
			next(){
				this.$emit('navigation',this.data.nextPageToken);
			},
			prev(){
				this.$emit('navigation',this.data.prevPageToken);
			}
		}
	}
</script>
<style type="text/css" scoped>
</style>