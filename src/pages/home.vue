<template>   
        <!-- 主页 --> 
    <div class="contanier">   
        <home-header></home-header> 
        <div class="wrapper">
            <div class="side"></div>
            <div class="main">
                <h2 class="lv">更多<span class="lvnei">(<router-link :to="luyou" class="link">更多</router-link>)</span><div class="side-control">
                    <div class="side-dots">
                        <div v-for="index in geshu" class="dot" :class="{ 'active':index==1 }" :data-index="index" :key="index"></div>
                    </div>
                    <span class="side-btn">
                        <div  class="prev"><</div>
                        <div  class="next">></div>
                    </span>
                </div></h2> 
                <div class="slide"> 
                    <div class="slideshow" style="width: 4050px;left: -675px">
                        <vm-ul v-for="(items,index) in dy" :mv="items.mv" :key="index"></vm-ul>
                    </div>
                </div>
            </div>
        </div>
        <foot></foot>
    </div>   
</template>  
<style scoped>  
    @import "../../static/css/home.css";
</style>  

<script>  
    // 导入要用到的子组件  
    import HomeHeader from '../components/HomeHeader'   
    import Foot from '../components/Foot'
    import List from '../components/List'
    import VmUl from '../components/VmUl'
    import {a} from '../../static/js/a.js'
    import {setCookie,getCookie} from '../../static/js/cookie.js'
    export default {  
        data () {  
            return { 
                name: "更多",
                luyou: "/detail", 
                mark: 0,
                geshu:[1,2,3,4],
                dy:[{mv:[]},{mv:[]},{mv:[]},{mv:[]},{mv:[]},{mv:[]}]
            }  
        },
        // 在components字段中，包含导入的子组件  
        components: {  
            HomeHeader,Foot,List,VmUl
        },
        created(){
                for(var j=0;j<6;j++){
                for(var i=0;i<10;i++){
                    this.$set(this.dy[j].mv,i,{lj:"/Ym5",name:"那些年",img:"../../static/img/dy/p1062824805.jpg",fenshu:"xx40",fen:"8.8"});
                }}
            $(function(){
                a();
            });
        }  
    } 
    
</script> 