<template>
    <div class="slider-wrapper" @mousemove="claerInv" @mouseout="runInv">
        <!-- 轮播图 -->
        <div v-show="index === nowIndex" v-for="(item,index) in sliderImgList" :key="index" class="slider-item" v-bind:class="['item'+[index+1]]">
            <a href="">
                <img v-bind:src=item.imgUrl alt="">
            </a>
        </div>
        <!-- 图片标题 -->
        <h2 class="slider-title">{{ sliderImgList[nowIndex].title }}</h2>
        <!-- 上一张下一张 -->
        <a v-on:click="preHandler" class="btn pre-btn" href="javascript:void(0)">&lt;</a>
        <a v-on:click="nextHandler" class="btn next-btn" href="javascript:void(0)">&gt;</a>
        <!-- dots -->
        <ul class="slider-dots">
            <li v-on:click="clickDots(index)" v-for="(item,index) in sliderImgList" :key='index'>{{ index+1 }}</li>
        </ul>
    </div>
</template>

<script>
export default {
    data() {
        return {
            nowIndex : 0,
            sliderImgList : [
                {
                    imgUrl:require('../assets/pic1.jpg'),
                    title:'第一张'
                    },
                {
                    imgUrl:require('../assets/pic2.jpg'),
                    title:'第二张'
                    },
                {
                    imgUrl:require('../assets/pic3.jpg'),
                    title:'第三张'
                    },
                {
                    imgUrl:require('../assets/pic4.jpg'),
                    title:'第四张'
                    }
                ]
        }
    },
    methods: {
        clickDots(index){
            this.nowIndex = index
        },
        preHandler(){
            this.nowIndex--;
            if(this.nowIndex < 0){
                this.nowIndex = 3
            }
        },
        nextHandler(){
            this.autoPlay()
        },
        autoPlay(){
            this.nowIndex++;
            if(this.nowIndex > 3){
                this.nowIndex = 0
            }
        },
        runInv(){
            this.invID = setInterval(this.autoPlay,1000)
        },
        claerInv(){
            clearInterval(this.invID)
        },
    },
    created() {
        this.runInv()
    },
}
</script>

<style scoped>
    .slider-wrapper{
        margin-top: 15px;
        width: 900px;
        height: 500px;
        /* overflow: hidden; */
        position: relative;
    }
    .slider-item{
        width: 900px;
        height: 500px;
        position: absolute;
    }
    .item1{
        z-index: 100;
    }
    .item2{
        z-index: 90;
    }
    .item3{
        z-index: 80;
    }
    .item4{
        z-index: 70;
    }
    .slider-dots{
        z-index: 200;
        position: absolute;
        right: 50px;
        bottom: 20px;
    }
    .slider-dots li{
        width: 20px;
        height: 20px;
        border-radius: 50%;
        text-align: center;
        line-height: 20px;
        background: #000;
        float: left;
        color: #ffffff;
        opacity: 0.6;
        margin: 0 10px;
    }
    .btn{
        width: 40px;
        height: 50px;
        /* background: #000; */
        color: #000;
        position: absolute;
        z-index: 300;
        top: 50%;
        margin-top: -25px;
        font-size: 40px;
        text-align: center;
        line-height: 50px;
    }
    .pre-btn{
        left: 10px;
    }
    .next-btn{
        right: 10px;
    }
    .slider-title{
        position: absolute;
        z-index: 400;
        bottom: 10px;
        left: 10px;
        font-size: 18px;
        color: #000;
        opacity: 0.6;
    }
</style>