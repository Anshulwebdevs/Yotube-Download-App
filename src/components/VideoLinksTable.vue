<template>
	<div class="col-md-8">
		<div v-if="info" class="row justify-content-md-center">
			<img :src="info.video.snippet.thumbnails.default.url" />

			<h6>{{ info.video.snippet.title }}</h6>
			<br />
		</div>
		<div class="row justify-content-md-center">
			<div class="col-md-12">
				<table v-if="LinksData" class="table table-striped">
					<tr>
						<th>Type</th>
						<th>Quality</th>
						<th>Link</th>
					</tr>
					<tr v-for="(item, index) in LinksData.data" :key="index">
						<td>{{ item.type }}</td>
						<td>{{item.quality}}</td>
						<td><a :href="item.url" :title="title(item.type)" download target="_button"><button class="btn">Download</button></a></td>
					</tr>
				</table>	
			</div>
				
		</div>
		
	</div>
</template>
<script type="text/javascript">
export default{
	name:"VideoLinksTable",
	data(){
		return {
			//infoArray
		};
	},
	props:['info'],
	methods:{
		// getInfo(response) {
		// 	var j = response; 
		// 	var obj = qs.parse(j);
		// 	var streams = obj.url_encoded_fmt_stream_map.split(",");
		// 	var infoArray = [];
		// 	streams.forEach((item)=>{
		// 		let obj = qs.parse(item);
		// 		obj.type = obj.type.split(";")[0].split("/")[1];
		// 		infoArray.push(obj);
		// 	});
		// 	return infoArray;
		// },
		title(ext){
			if(this.info){
				return this.info.video.snippet.title.replace(/ /g,"_") + "." +ext;
			}
		}
	},
	computed:{
		LinksData(){
			if(this.info){
				return this.info;
			}
		}
	}
}
</script>
<style type="text/css" scoped>

</style>