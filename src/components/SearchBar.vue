<template>
	<div >
		<!-- <form @submit="onSubmit"> -->
		<input class="form-control" @input="onInput" autocomplete="off"/>
		<!-- <input class="form-control" name="query" autocomplete="off"/> -->
		<!-- <button class="btn btn-default" type="submit">Search</button> -->
		<!-- </form> -->
	</div>
</template>
<script type="text/javascript">
	export default{
		name:"SearchBar",
		methods:{
			// onSubmit: function(event){
			// 	event.preventDefault();
			// 	this.$emit('termChange',event.target.elements.query.value);
			// },
			onInput: function(event){
				this.$emit('termChange',event.target.value);
			}


		}
	};
</script>
<style type="text/css" scoped>

div{
	text-align: center;
	margin: 20px;
}
</style>