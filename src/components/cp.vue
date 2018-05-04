<template>  
<!-- 电影详情页的长评组件 --> 
    <div class="contanier" :mid="mid" :uid="uid">   
        <div v-show="xsm">
            <h2 class="lv" :name="name">{{name}}的剧评· · · · · ·</h2>
            <button v-for="(item,index) in bt" class="bt" :class="{'hou':item.cc}" :key="index" @click="dj(index)">{{item.name}}</button>
            <div v-if="xsf==1" class="lb">
                <gdcul :lb="lb" :uid="uid"></gdcul>
                <a href="javascript:;" class="show" @click="gd" v-show="qbdp">>更多短评{{gs}}条</a>
            </div>
            <div v-else class="wbc">该电影暂无剧评</div>
        </div>
    </div>   
</template>

<style scoped>
.hou{
    background: #f2fbf2;
}
.wbc{
    border: 1px solid #aaffaa;
    background: #f2fbf2;
    border-left: 0;
    border-right: 0;
    text-align: center;
    padding: 4px 0 3px;
    color: #494949;
    margin: 15px 0;
}
</style>

<script>
    import {setCookie,getCookie} from '../../static/js/cookie.js'
    import gdcul from './gdcul'
    export default{
        components: {  
            gdcul
        },
        props: ['name','mid','uid'],
        data(){
            return{
                xsm:true,
                xsf:1,
                qbdp:false,
                gs:"",
                bt:[{name:"热门",cc:true},{name:"最新",cc:false},{name:"好友",cc:false}],
                lb:[],
                gjc:"热门",
            }
        },
        methods:{
            //该电影长评超过电影详情页长评限制数，点击至该电影全部长评页面
            gd(){
                this.$router.push({path:'/qbcp',query:{gjc:'热门',name:this.name,mid:this.mid,uid:this.uid,dp:0}});
            },
            //长评按热门或是最新排序
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
            //将后台传来的数据呈现在页面
            hh(){
                
                        this.xsf=1;
                        for(var i=0;i<1;i++){
                            this.$set(this.lb,i,{lj:"",name:"小老百姓呐",sj:"2018-09-21",fenshu:"xx50",content:"今儿老百姓呀，真呀真高兴呐。完成了人生中第一个还算比较完整项目的我，觉得浑身上下充满了拯救了世界一般的成就感,虽然还有很多的不足之处，但有不足之处才会有进步的空间，才会有学习的机会。要不然人生平平淡淡，没有挑战之事，会是多么索然无味。说实话，2014年第一次入大学，深受高中老师经典语录之——上了大学就可以想怎么玩怎么玩了——的影响，考上一所平平淡淡大学的我，自以为很聪明能上个不平凡大学的我，在高考结束一秒便删除所有关于学习记忆的我，终究没有激起心中的不甘，开始了吃饭睡觉打豆豆的堕落大学生活。没有了老师家长的管束，生活可以要多自在有多自在。于是，关于大学没有过挂科是遗憾这种鬼话，在我光荣挂了一门微观经济学之后，为了安慰脸皮还不够厚的自己，我硬是厚脸皮地相信了。。。颓废的日子过久了便觉得厌烦，漫画、游戏、画画、书法渐渐地都不能缓解生活的乏味了。你以为我会变得更颓废吗，哼哼。。。没错是这样的。时光如流水，本以为大学四年将会这样过去，这个时候，在我眼里如男神一般的老师出现了，网站建设老师，他的幽默风趣以及聪明的头脑，令我着迷，于是我鼓起勇气向他表达了我的心意，知道我对它的爱意之后，男神老师引领我，走上了追求它——前端开发（盖房子）的道路，一去不复返。打好HTML，css，JavaScript三大基石后，在PHP商店里取了盖房原材料，在vue和jQuery框架的帮助下，盖起了这间小房。虽然看起来摇摇欲坠，但不管大神有多少，我有多小白，它有多烧我的脑，多伤我的心，我还是如此爱它，因为它让我的脑子可以不用像破铜烂铁一般荒置，并让我如同打了鸡血般不知疲倦。每完成一项功能，都能让我在上一秒的我面前狂吹牛x，让我感受到了源源不断的快乐。所以，追求前端开发这条道路，我将会孜孜不倦地走下去，直到有一天，有地方能够认可我。",hzs:999,mys:0,biaoti:"菜鸟说",xx:true,fold:true,up:"../../static/img/xx/up.png",down:"../../static/img/xx/down.png"});
                        }
            }
        },
        created(){
            this.hh();
        }
    }
</script>