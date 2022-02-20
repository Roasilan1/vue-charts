<template>
    <div class="echarts">

    </div>
</template>

<script>
const echarts = require("echarts");
import BASE_OPTIONS from "./options/BaseOption.json";
import {merge} from "lodash";

export default {
    props:{
        seriesData:{//数据
            type:Array,
            required:true,
            //默认是一个函数... 返回一个数组的函数  
            default:()=>[]
        },
        extraOptions:{//配置项
            type:Object,
            //拓展属性默认返回的是一个函数  函数返回的是对象
            default:()=>({})
        },
    },
    data(){
        return {
            chart:null
        }
    },
    watch:{
        series:{
            deep:true,
            handler(){
                //series变化则更新echart视图
                this.refreshView();
            }
        }
    },
    mounted(){
        //这里设置echart实例到instance中
        this.chart=echarts.init(this.$el);
        this.refreshView();
    },
    methods:{
        refreshView(){
            if(!this.chart)
                return;
            //合并数据到配置项当中
            const fullOption=this.mergeDataToOption();
            console.log(fullOption);

            //设置
            this.chart.setOption(fullOption,true);
        },
        mergeDataToOption(){
            return merge(
                {},
                BASE_OPTIONS,
                {
                    series:[{data:this.seriesData}]
                },
                this.extraOptions
            )
        }
    }
}
</script>
<style scoped>
.echarts{
    width: 100%;;
    height: 100%;
}
</style>