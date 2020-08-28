<template lang="html">
  <div class="nine">
   	<div class="weixin">
   		<img src="../assets/logo-ea5.png" />
   		<span>请登录</span>
   	</div>
  </div>
</template>

<script>
export default {
	name:"nine",
	data(){
		return{
			
		}
	},
	methods:{
		
	}
}
</script>

<style scoped>
	.weixin{
		/*border:1px solid red;*/
		height:100px;
		width: 100%;
		background-color: white;
		border-bottom: 1px solid #e5e5e5;
		cursor: pointer;
	}
	.weixin img{
		/*display: inline-flex;
		margin-left: 10x;*/
		height: 80%;
		float: left;
		margin-left: 30px;
		margin-top: 10px;
	}
	.weixin span{
		display: inline-block;
		margin-top: 38px;
		margin-left: 10px;
	}
</style>
