<template>
    <div class="content">
        <h1>{{$route.params.title}}</h1>
        <div class="close" @click='close'>X</div>
        <p v-html="content"></p>
    </div>
</template>

<script>
import util from '../api/getData'

export default {
    data() {
        return {
            content:''
        }
    },
    methods: {
        _getContent(url){
            
            util.getContent(url).then(data=>{
                this.content = data;
            })

        },
        close(){
            this.$router.back();
        }
    },
    created() {
        // console.log(this.$route.params);
        let url = this.$route.params.url;
        this._getContent(url);
    },
}
</script>

<style scoped>
.content{
    position: absolute;
    top: 0;left: 0;right: 0;bottom: 0;
    z-index: 2;
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
p{
    text-align: left;
    margin-left: 10px;
    height: 500px;
    overflow: scroll;
}
</style>