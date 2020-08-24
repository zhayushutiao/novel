<template>
    <div class="show">
        <ul>
            <li v-for="(item,i) in lists" :key="i" value="i">
                <div class="image" @click="choose(item)">
                        <img :src="item.img" height="150" width="120">
                </div>
                <dl>
                    <dt>
                        <span class="author">{{item.author}}</span>
                        <span @click="choose(item)">{{item.name}}</span>
                    </dt>
                    <dd>{{item.desc}}</dd>
                </dl>
            </li>
        </ul>
        <router-view></router-view>
    </div>
</template>

<script>
import util from '../api/getData'

export default {
    data() {
        return {
            lists:[]
        }
    },
    created() {
        // 获取id
        let id = this.$route.params.id;
        this._getNovelList(id)
    },
    beforeRouteUpdate (to, from, next) {
        this._getNovelList(to.params.id)
        next()
    },
    methods: {
        _getNovelList(id){
            util.getNovelList(id).then(data=>{
                this.lists = data;
            }).catch(err=>{
                console.log(err);
            })
        },
        choose(item){
            // 切换路由到某小说列表组件
            // console.log(item);
            // 使用编程式导航切换路由
            // let id = this.$route.params.id;
            this.$router.push({
                name:'chapter',
                params:{
                    url:item.path,
                    name:item.name
                }
            })
        }
    },
}
</script>

<style scoped>
*{margin: 0;padding: 0;}
.show{position: relative;}
ul li{list-style: none;}
ul{ border:3px solid #C8D4E1; margin: 10px auto; padding:5px; width:964px; height:320px; overflow:hidden;}
li{ width:315px; float:left; padding:5px 0px 0px 5px;}
.image{ float:left; width:120px;}
.image img{ border:solid 1px #DDDDDD; padding:1px; background-color:White;}
dl{ padding:0px 5px 0px 0px; float:right; width:180px;}
dl dt{ height:25px; line-height:25px; overflow:hidden; font-size:14px; border-bottom:dotted 1px #6191D0; font-weight:bold; }
dl dt .author{ float:right; font-weight:normal;}
dl dd{ padding:7px 0px 0px 0px; line-height:20px; color:#9E9E9E; text-indent:2em; height:125px; overflow:hidden;font-size: 13px;}
</style>