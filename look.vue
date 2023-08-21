<template>
  <div class="look">
    <div v-show="isNotFound">对不起，你搜索的城市暂无数据或搜索错误，请重新输入！</div>
    <div v-show="weather.isShow">
    <img :src="weather.imgPath" class="look-icon">
    <h1 class="temp">{{weather.temp}}℃</h1>
    <h2 class="city">{{weather.city}}</h2>
    <div class="details">
        <div class="col">
            <img src="" />
            <div>
                <p class="humidity">{{weather.humidity}}%</p>
                <p>湿度</p>
            </div>
        </div>
        <div class="col">
            <img src="">
            <div>
                <p class="wind">{{weather.windSpeed}} 米/秒</p>
                <p>风力</p>
            </div>
        </div>
    </div>
    </div>
  </div>
</template>

<script>
export default {
    name:'look',
    data(){
        return{
            weather:{},
            isNotFound:{}
        }
    },
    methods:{
        displayWeather(weather,isNotFound){
            this.weather=weather,
            this.isNotFound=isNotFound
        },
        isNotFound(isNotFound){
            this.isNotFound=isNotFound
        }
    },
    mounted(){
        this.$bus.$on('displayWeather',this.displayWeather)
        this.$bus.$on('displayisNotFound',this.displayisNotFound)
    }
}
</script>

<style lang="css" scoped>
.look-icon{
    width: 170px;
    margin-top: 30px;

}
.look h1{
    font-size: 80px;
    font-weight: 500;
}
.look h2{
    font-size:45px;
    font-weight: 400;
    margin-top: -10px;
}
.details{
    display: flex;
    align-content: space-between;
    padding: 0 20px;
    margin-top: 50px;
}
.col{
    display: flex;
    align-items: center;
    text-align: left;
}
.col img{
    width: 40px;
    margin-right: 10px;
}
.humidity,.wind{
    font-size: 28px;
    margin-top: -6px;
}
</style>