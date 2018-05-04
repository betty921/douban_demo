<template>
	<li class="sec_li" :luyou="luyou" :img="img" :name="name" :fenshu="fenshu" :fen="fen">
		<router-link :to="luyou" class="link1">
			<img class="tu" :src="img">
		</router-link>	
		<div class="miaoshu">
			<router-link :to="luyou" class="link2">{{ name }}</router-link>
		</div>
		<div class="rating">
			<span class="xing" :class="fenshu"></span><i>{{ fen }}</i>
		</div>	
	</li>
</template>

<style scoped>
	@import "../../static/css/xiaox.css";
	@import "../../static/css/list.css";
</style>
<script>
	export default{
		props: ['luyou','img','name','fen','fenshu']
	}
</script>