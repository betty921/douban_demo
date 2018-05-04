<template> 
<!-- 电影全部短评页面 -->   
    <div class="contanier">  
        <home-header></home-header> 
        <div class="wrapper">
            <div class="side"></div>
            <div class="main"> 
                <div>
                    <h2 class="h2" style="margin-bottom:10px;">{{this.$route.query.name}}的短评</h2>
                    <button v-for="(item,index) in bt" class="bt" :class="{'hou':item.cc}" :key="index" @click="dj(index)">{{item.name}}</button>
                    <div class="lb">
                        <dpul :lb="lb" :uid="uid"></dpul>
                    </div>
                    <fy :num='num' :limit='limit' :offset='offset' :uid='uid' :name='name' :mid='mid' :path="path" :gjc="gjc"></fy>
                </div>
            </div>
        </div>
        <foot></foot>
    </div>   
</template>

<style scoped>
    .hou{
        background: #f2fbf2;
    }
</style>

<script>
    import HomeHeader from '../components/HomeHeader'
    import Foot from '../components/Foot'
    import dpul from '../components/dpul'
    import fy from '../components/fy'
    export default{
        components: {  
            HomeHeader,Foot,dpul,fy
        },
        data(){
            return{
                num: 9,
                limit: 5,
                offset:0,
                bt:[{name:"热门",cc:true},{name:"最新",cc:false},{name:"好友",cc:false}],
                lb:[],
                gjc:"热门",
                uid:-1,
                mid:-1,
                name:"",
                path:"/qbdp"
            }
        },
        methods:{
            //短评排序方式
            dj(i){
                this.bt[i].cc=true;
                switch(i){
                    case (0):
                        this.bt[1].cc=false;
                        this.bt[2].cc=false;
                        this.gjc="热门";
                        break;
                    case (1):
                        this.bt[0].cc=false;
                        this.bt[2].cc=false;
                        this.gjc="最新";
                        break;
                    case (2):
                        this.bt[1].cc=false;
                        this.bt[0].cc=false;
                        this.gjc="好友";
                        break;                      
                }
                this.hh();
            },
            //将后台传来的json数据渲染至相关dom
            hh(){
                this.offset=parseInt(this.$route.query.dp);
                this.uid=this.$route.query.uid;
                this.mid=this.$route.query.mid;
                this.name=this.$route.query.name;
                    if(this.offset==0){
                        for(var i=0;i<5;i++){
                             this.$set(this.lb,i,{lj:"",name:"叶语",sj:"2018-09-21",fenshu:"xx45",content:"小生经验不足，还请多指教",hzs:666,xx:true});
                        }
                    }
                    else{
                        this.lb=[];
                        for(var i=0;i<4;i++){
                             this.$set(this.lb,i,{lj:"",name:"二丫",sj:"2018-09-21",fenshu:"xx45",content:"好运来祝你好运来",hzs:666,xx:true});
                        }
                    }
            }
        },
        created(){
            this.hh();
        },
        watch:{
            '$route':'hh'
        }
    }
</script>