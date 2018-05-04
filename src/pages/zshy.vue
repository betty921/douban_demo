<template>   
<!-- 所有电影中最受欢迎的长评页面 -->
    <div class="contanier">  
        <home-header></home-header> 
        <div class="wrapper">
            <div class="side"></div>
            <div class="main"> 
                <div>
                    <h2 class="h2">豆瓣最受欢迎的影评</h2>
                    <button v-for="(item,index) in bt" class="bt" :class="{'hou':item.cc}" :key="index" @click="dj(index)">{{item.name}}</button>
                    <div class="lb">
                        <ul class="lbul">
                            <li v-for="(item,index) in lb" :key="index" v-show="item.xx">                               
                                <router-link :to="item.ljt" style="font-size:0px;display:block;">
                                    <img :src="item.img" width="75px" style="float:left;margin-right:20px;">
                                </router-link>
                                <div style="padding-left:95px;">
                                    <router-link to="" class="lp_li_a">{{item.name}}</router-link>
                                    <span class="xing" :class="item.fenshu"></span><span class="sj">{{item.sj}}</span>
                                    <p style="color: #3388c4;">{{item.biaoti}}</p>
                                    <p class="msg" style="display:inline;font-size:13px">{{item.fold?maxSlice(item.content):item.content}}</p>
                                    <div v-show="item.content.length>maxLength" style="display:inline;">
                                        <a href="javascript:;" class="show" @click="item.fold=false" v-show="item.fold" style="vertical-align:1px;">展开</a>
                                        <a href="javascript:;" class="show" @click="item.fold=true" v-show="!item.fold" style="vertical-align:1px;">收起</a>
                                    </div>
                                    <div class="yymy">
                                        <a href="javascript:;" class="ym-btn" @click="ymy(item.lj,index,1,item.up)">
                                            <img :src="item.up" width="12px">
                                            <span>{{item.hzs}}</span>
                                        </a>
                                        <a href="javascript:;" class="ym-btn" @click="ymy(item.lj,index,2,item.down)">
                                            <img :src="item.down" width="12px">
                                            <span>{{item.mys}}</span>
                                        </a>
                                    </div>
                                </div>
                            </li>
                        </ul>
                    </div>
                    <div class="qyhy">
                        <fy :num='num' :limit='limit' :offset='offset' :uid='uid' :name='name' :mid='mid' :path="path" :gjc="gjc"></fy>
                    </div>
                </div>
            </div>
        </div>
        <foot></foot>
    </div>   
</template>

<style scoped>
    @import "../../static/css/plgy.css";
    @import "../../static/css/cp.css";
    @import "../../static/css/xiaox.css";
</style>

<script>
    import {setCookie,getCookie} from '../../static/js/cookie.js'
    import HomeHeader from '../components/HomeHeader'
    import Foot from '../components/Foot'
    import fy from '../components/fy'
    export default{
        components: {  
            HomeHeader,Foot,fy
        },
        data(){
            return{
                num: 2,
                limit: 1,
                offset:0, 
                uid:-1, 
                mid:-1,
                name:"",
                path:"/zshy",  
                maxLength:120, 
                gjc:"热门",          
                bt:[{name:"热门",cc:true},{name:"最新",cc:false}],
                lb:[],
            }
        },
        methods:{
            maxSlice(v){
                return v.length>this.maxLength?v.slice(0,this.maxLength)+'...':v;
            },
            ymy(a,i,j,b){
                if(this.uid!=-1){
                    if(j==1&&b=="../../static/xx/up.png"){
                        let data={'dpid':a,'uid':this.uid,'ymy':j};
                        this.$http.post('http://localhost/douban/pl/ymy.php',data,{emulateJSON:true})
                        .then((res)=>{
                            console.log(res);
                            this.lb[i].hzs=res.data.hzs;
                            this.lb[i].mys=res.data.mys;
                            this.lb[i].up="../../static/xx/uph.png";
                            this.lb[i].down="../../static/xx/down.png";
                        });
                    }
                    if(j==2&&b=="../../static/xx/down.png"){
                        let data={'dpid':a,'uid':this.uid,'ymy':j};
                        this.$http.post('http://localhost/douban/pl/ymy.php',data,{emulateJSON:true})
                        .then((res)=>{
                            console.log(res);
                            this.lb[i].hzs=res.data.hzs;
                            this.lb[i].mys=res.data.mys;
                            this.lb[i].down="../../static/xx/downh.png";
                            this.lb[i].up="../../static/xx/up.png";
                        });
                    }
                }
            },
            gg(){
                this.uid=getCookie('userid');
                if(this.$route.query.dp>=0){
                    this.offset=parseInt(this.$route.query.dp);
                }else{this.offset=0;}
                    if(this.offset==0){
                        for(var i=0;i<1;i++){
                            this.$set(this.lb,i,{lj:"",name:"小老板姓呐",sj:"2018-09-21",fenshu:"xx50",content:"今儿老百姓呀，真呀真高兴呐。完成了人生中第一个还算比较完整项目的我，觉得浑身上下充满了拯救了世界一般的成就感,虽然还有很多的不足之处，但有不足之处才会有进步的空间，才会有学习的机会。要不然人生平平淡淡，没有挑战之事，会是多么索然无味。说实话，2014年第一次入大学，深受高中老师经典语录之——上了大学就可以想怎么玩怎么玩了——的影响，考上一所平平淡淡大学的我，自以为很聪明能上个不平凡大学的我，在高考结束一秒便删除所有关于学习记忆的我，终究没有激起心中的不甘，开始了吃饭睡觉打豆豆的堕落大学生活。没有了老师家长的管束，生活可以要多自在有多自在。于是，关于大学没有过挂科是遗憾这种鬼话，在我光荣挂了一门微观经济学之后，为了安慰脸皮还不够厚的自己，我硬是厚脸皮地相信了。。。颓废的日子过久了便觉得厌烦，漫画、游戏、画画、书法渐渐地都不能缓解生活的乏味了。你以为我会变得更颓废吗，哼哼。。。没错是这样的。时光如流水，本以为大学四年将会这样过去，这个时候，在我眼里如男神一般的老师出现了，网站建设老师，他的幽默风趣以及聪明的头脑，令我着迷，于是我鼓起勇气向他表达了我的心意，知道我对它的爱意之后，男神老师引领我，走上了追求它——前端开发（盖房子）的道路，一去不复返。打好HTML，css，JavaScript三大基石后，在PHP商店里取了盖房原材料，在vue和jQuery框架的帮助下，盖起了这间小房。虽然看起来摇摇欲坠，但不管大神有多少，我有多小白，它有多烧我的脑，多伤我的心，我还是如此爱它，因为它让我的脑子可以不用像破铜烂铁一般荒置，并让我如同打了鸡血般不知疲倦。每完成一项功能，都能让我在上一秒的我面前狂吹牛x，让我感受到了源源不断的快乐。所以，追求前端开发这条道路，我将会孜孜不倦地走下去，直到有一天，有地方能够认可我。",hzs:"999",mys:"0",biaoti:"菜鸟说",xx:true,fold:true,up:"../../static/img/xx/up.png",down:"../../static/img/xx/down.png",ljt:"/Ym05",img:"../../static/img/dy/p1062824805.jpg"});
                        }
                    }
                    else{
                    this.lb=[];
                    for(var i=0;i<1;i++){
                        this.$set(this.lb,i,{lj:"",name:"hiahia",sj:"2018-09-21",fenshu:"xx50",content:"今儿老百姓呀，真呀真高兴呐。完成了人生中第一个还算比较完整项目的我，觉得浑身上下充满了拯救了世界一般的成就感,虽然还有很多的不足之处，但有不足之处才会有进步的空间，才会有学习的机会。要不然人生平平淡淡，没有挑战之事，会是多么索然无味。说实话，2014年第一次入大学，深受高中老师经典语录之——上了大学就可以想怎么玩怎么玩了——的影响，考上一所平平淡淡大学的我，自以为很聪明能上个不平凡大学的我，在高考结束一秒便删除所有关于学习记忆的我，终究没有激起心中的不甘，开始了吃饭睡觉打豆豆的堕落大学生活。没有了老师家长的管束，生活可以要多自在有多自在。于是，关于大学没有过挂科是遗憾这种鬼话，在我光荣挂了一门微观经济学之后，为了安慰脸皮还不够厚的自己，我硬是厚脸皮地相信了。。。颓废的日子过久了便觉得厌烦，漫画、游戏、画画、书法渐渐地都不能缓解生活的乏味了。你以为我会变得更颓废吗，哼哼。。。没错是这样的。时光如流水，本以为大学四年将会这样过去，这个时候，在我眼里如男神一般的老师出现了，网站建设老师，他的幽默风趣以及聪明的头脑，令我着迷，于是我鼓起勇气向他表达了我的心意，知道我对它的爱意之后，男神老师引领我，走上了追求它——前端开发（盖房子）的道路，一去不复返。打好HTML，css，JavaScript三大基石后，在PHP商店里取了盖房原材料，在vue和jQuery框架的帮助下，盖起了这间小房。虽然看起来摇摇欲坠，但不管大神有多少，我有多小白，它有多烧我的脑，多伤我的心，我还是如此爱它，因为它让我的脑子可以不用像破铜烂铁一般荒置，并让我如同打了鸡血般不知疲倦。每完成一项功能，都能让我在上一秒的我面前狂吹牛x，让我感受到了源源不断的快乐。所以，追求前端开发这条道路，我将会孜孜不倦地走下去，直到有一天，有地方能够认可我。",hzs:"999",mys:"0",biaoti:"小黑说",xx:true,fold:true,up:"../../static/img/xx/up.png",down:"../../static/img/xx/down.png",ljt:"/Ym5",img:"../../static/img/dy/p1062824805.jpg"});
                    }}
            },
            dj(i){
                this.bt[i].cc=true;
                switch(i){
                    case (0):
                        this.bt[1].cc=false;
                        this.gjc="热门";
                        break;
                    case (1):
                        this.bt[0].cc=false;
                        this.gjc="最新";
                        break;                     
                }
                this.gg();
            }
        },
        created(){
            this.gg();
        },
        watch:{
            '$route':'gg'
        }
    }
</script>