<template>
  <div class="copy">
    <input type="text" placeholder="请输入城市名字" spellcheck="false" v-model="cityName">
    <button @click="copy"><img src=""></button>
  </div>
</template>

<script>
import axios from'axios'
export default {
    name:'copy',
    data(){
        return{
            cityName:''
        }
    },
    methods:{
        copy(){
            if(!this.cityName.trim()) return
            const apiKey="78b262ed7919f0d79a2ca50a4a6f82bf"
            const apiUrlGetLatAndLon=`http://api.openweathermap.org/geo/1.0/direct?q=${this.cityName}&appid=${apiKey}`
            axios.get(apiUrlGetLatAndLon).then(
                response=>{
                console.log('响应式数据：',response.data)
                if(!response.data.length) {
                this.$bus.$emit('dispalyNotFound',ture)
                }else{
                        const lat =response.data[0].lat
                        console.log('纬度',lat)
                        const lon =response.data[0].lon
                        console.log('经度',lon)
                        const apiUrlGetWeather=`https://api.openweathermap.org/data/2.5/weather?lat=${lat}&1on=${lon}&appid=${apiKey}`
                        axios.get('apiUrlGetWeather').then(
                            response=>{
                                console.log('响应式数据：',response.data)
                                const weather={
                                    imgPath:`https://openweathermap.org/img/wn/${response.data.weather[0].icon}@2x.png`,
                                    temp: response.data.main.temp,
                                    humidity: response.data.wind.spend,
                                    windSpeed:response.data.wind.spend,
                                    city:this.cityName,
                                    isShow:true,
                        }
                        this.$bus.$emit('displayWeather',weather,false)
                    },
                    error=>{
                        console.log('错误信息为：',error.message)
                    }
                )
                }
            },
            error=>{
                console.log('错误信息为：',error.message)
            }
            )
        }
    }
}
</script>

<style lang="css" scoped>
.copy{
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;

}
.copy input{
    border: 0;
    outline: 0;
    background: #ebfffc;
    color: #555;
    padding: 10px 25px;
}
.copy button{
    border: 0;
    outline: 0;
    background: #ebfffc;
    border-radius: 50%;
    width: 60px;
    height: 60px;
    cursor: pointer;
}
.copy button img{
    width: 16rpx;
}
</style>