<template>
<!-- 主页的轮播组件 -->
	<ul :mv="mv" class="hh">
		<list v-for="(item,index) in mv"
      	:luyou="item.lj"
      	:img="item.img"
      	:name="item.name"
      	:fenshu="item.fenshu"
      	:fen="item.fen"
      	:key="index">
		</list>
	</ul>
</template>
<style scoped>
	.hh{
		width: 700px;
		margin: 0 -25px 0 0;
	}
</style>
<script>
	import List from './List'
	export default{
		props: ['mv'],
		components: {  
            List
        } 
	}
</script>