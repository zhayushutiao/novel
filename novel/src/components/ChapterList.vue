<template>
    <div class="chapter container-fluid">
        <h1>{{$route.params.name}}</h1>
        <div class="close" @click="close">X</div>
        <div class="row">
            <div v-for="(c,i) in chapters" :key="i" class="col-sm-4" @click="choose(c)">
                {{c.title}}
            </div>
        </div>
        <router-view></router-view>
    </div>
</template>

<script>
import util from '../api/getData'
export default {
    data() {
        return {
            chapters:[]
        }
    },
    methods: {
        _getChapter(){
            // console.log(this.$route.params);
            let url = this.$route.params.url;
            util.getChapter(url).then(data=>{
                this.chapters = data;
            })
        },
        close(){
            // this.$router.go(-1);
            this.$router.back();
        },
        choose(chapter){
            // 切换路由到某个章节组件
            this.$router.push({
                name:'content',
                params:{
                    url:chapter.url,
                    title:chapter.title
                }
            })
        }
    },
    created() {
        this._getChapter();
    },
}
</script>

<style scoped>
.chapter{
    position: absolute;
    top: 0;left: 0;right: 0;bottom: 0;
    z-index: 1;
    width: 100%;
    height: 550px;
    background-color: cadetblue;
    padding: 0;
}
.close{
    width: 20px;height: 20px;
    position: absolute;
    top: 15px;right: 25px;
    cursor: pointer;
}
.row{
    text-align: left;
    height: 500px;
    overflow: scroll;
    margin-left: 0;
    margin-right: 0;
  }
  .row>div{
    border-bottom: 1px dashed #CCCCCC;
    height: 25px;
    line-height: 200%;
    margin-bottom: 5px;
    text-indent: 10px;
    vertical-align: middle;
    cursor: pointer;
  }
  .row>div:hover{
    color:#6F78A7;
  }
</style>