<template>
    <div class="content">

        <div class="title-div main-bg">
            <span class="title-text">宁波大学2017年迎新实时大数据</span>
            <div class="time-div">
                <i class="iconfont icon-shijian"></i>
                <span>{{ curTime }}</span>
            </div>
        </div>

        <div class="middle-div">

            <div class="left-div main-bg">
                <span class="left-div-title">各学院报道完成率</span>
                <span class="left-div-sub-title">some english here</span>
                <div class="left-div-content-div scroll-bar">
                    <div v-for="n in 20" class="p-10">
                        <div class="tal">
                            <span class="no-text">NO.{{ n }}</span>
                            <span class="no-name-text">XXX学院</span>
                        </div>
                        <div class="no-progress-bg">
                            <div class="no-progress" :style="{ width: n + '%' }"></div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="left2-div main-bg">
                <div id="map-chart" class="map"></div>
                <div class="left2-content-div">
                    <div class="left2-title1">
                        <span class="left2-title1-label">实时报到人数</span>
                        <span class="left2-title1-num">2222</span>
                        <span class="left2-title1-ren">人</span>
                    </div>
                    <div class="left2-title2">
                        <span class="left2-title2-label">实时报到比例</span>
                        <span class="left2-title2-num">56.7%</span>
                    </div>
                </div>
            </div>

            <div class="right-div">
                <div class="right-content1 main-bg">
                    <div class="right-content1-title-div">
                        <div class="right-content1-title-area">
                            <span class="right-content1-title">本科生报道率</span>
                            <span class="right-content1-sub-title">some english here</span>
                        </div>
                        <div class="right-content1-num-div">
                            <span class="right-content1-num-text">\</span>
                            <span class="right-content1-num">01</span>
                        </div>
                    </div>
                    <div id="ring-chart" class="ring-chart"></div>
                    <div class="right-content1-item1-div main-bg">
                        <span class="right-content1-item1-title">一季度销售额</span>
                        <span class="right-content1-item1-num">1321</span>
                        <span class="right-content1-item1-wan">万</span>
                    </div>
                    <div class="right-content1-item2-div main-bg">
                        <span class="right-content1-item2-title">同比增长</span>
                        <span class="right-content1-item2-jia">+</span>
                        <span class="right-content1-item2-num">150%</span>
                    </div>
                </div>

                <div class="right-content2 main-bg">
                    <div class="right-content2-content">
                        <div class="right-content2-title-div">
                            <span class="right-content2-title">各楼宇报道完成率</span>
                            <span class="right-content2-sub-title">some english here</span>
                        </div>
                        <div class="right-content2-num-div">
                            <span class="right-content2-num-text">\</span>
                            <span class="right-content2-num">04</span>
                        </div>
                        <div class="right-content2-data-list scroll-bar">
                            <div v-for="n in 10" class="mt-10">
                                <span class="right-content2-data-list-item-title">上海</span>
                                <div class="right-content2-data-list-item-progress-bg">
                                    <div class="right-content2-data-list-item-progress"
                                         :style="{ width: n*10 + '%' }"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="right2-div">
                <div class="right2-content1 main-bg">
                    <div class="right2-content1-div">
                        <div class="right2-content1-title-div">
                            <span class="right2-content1-title">财务缴费情况</span>
                        </div>
                    </div>
                    <div id="pie-chart" class="pie-chart"></div>
                </div>

                <div class="right2-content2 main-bg">
                    <div class="right2-content2-div">
                        <div class="right2-content2-title-div">
                            <span class="right2-content2-title">各时间段报道量</span>
                        </div>
                    </div>
                    <div id="line-chart-1" class="line-chart-1"></div>
                </div>
            </div>
        </div>

        <div class="bottom-div">
            <div class="bottom1-div bottom-bg">
                <img src="../../assets/logo.png" class="logo">
            </div>
            <div class="bottom2-div bottom-bg">
                <div class="bottom2-div-title-area">
                    <div class="bottom2-div-title-div">
                        <span class="bottom2-div-title">绿色通道办理情况</span>
                    </div>
                </div>
                <div id="line-chart-2" class="line-chart-2"></div>
            </div>
            <div class="bottom3-div bottom-bg">
                <div class="bottom3-div-title-area">
                    <div class="bottom3-div-title-div">
                        <span class="bottom3-div-title">实时报道人员</span>
                    </div>
                </div>
                <div class="bottom3-div-content">
                    <div v-for="n in 3" class="bottom3-div-content-item">
                        <div>
                            <span class="bottom3-div-content-item-text">企业经营指标1</span>
                            <span class="bottom3-div-content-item-num">12581万元</span>
                        </div>
                        <div class="mt-20">
                            <span class="bottom3-div-content-item-text">企业经营指标1</span>
                            <span class="bottom3-div-content-item-num">12581万元</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script type="text/javascript">
    import Utils from '../../utils';
    import $ from 'jquery';
    import echarts from 'echarts';
    import 'echarts/lib/chart/map';
    import '../../china';
    import '../../shine';

    export default {
        data() {
            return {
                curTime: ''
            }
        },
        components: {},
        created() {
            this.intervalid = setInterval(() => {
                let today = new Date();
                //分别取出年、月、日、时、分、秒
                let year = today.getFullYear();
                let month = today.getMonth() + 1;
                let day = today.getDate();
                let hours = today.getHours();
                let minutes = today.getMinutes();
                let seconds = today.getSeconds();
                //如果是单个数，则前面补0
                month = month < 10 ? "0" + month : month;
                day = day < 10 ? "0" + day : day;
                hours = hours < 10 ? "0" + hours : hours;
                minutes = minutes < 10 ? "0" + minutes : minutes;
                seconds = seconds < 10 ? "0" + seconds : seconds;
                //构建要输出的字符串
                this.curTime = year + "-" + month + "-" + day + " " + hours + ":" + minutes + ":" + seconds;
            }, 1000);
        },
        methods: {},
        watch: {},
        beforeDestroy() {
            clearInterval(this.intervalid)
        },
        mounted() {
            //地图图表
            let mapChart = echarts.init(document.getElementById('map-chart'), 'shine');
            let mapChartOption = {
                tooltip: {
                    trigger: 'item'
                },
                legend: {
                    orient: 'vertical',
                    top: 'bottom',
                    left: 'right',
                    data: ['iphone'],
                    textStyle: {
                        color: '#fff'
                    },
                    show: false
                },
                visualMap: {
                    min: 0,
                    max: 1000,
                    left: 'left',
                    top: 'bottom',
                    text: ['高', '低'],// 文本，默认为数值文本
                    inRange: {
                        color: ['#e0ffff', '#006edd']
                    },
                    textStyle: {
                        color: '#fff'
                    },
                    calculable: true,
                    show: false
                },
                series: [
                    {
                        name: 'iphone',
                        type: 'map',
                        mapType: 'china',
                        roam: false,
                        label: {
                            normal: {
                                show: true,
                                textStyle: {
                                    color: 'rgba(255, 255, 255, 1)'
                                }
                            },
                            emphasis: {
                                show: true
                            }
                        },
                        data: [
                            {name: '北京', value: Math.round(Math.random() * 1000)},
                            {name: '天津', value: Math.round(Math.random() * 1000)},
                            {name: '上海', value: Math.round(Math.random() * 1000)},
                            {name: '重庆', value: Math.round(Math.random() * 1000)},
                            {name: '河北', value: Math.round(Math.random() * 1000)},
                            {name: '河南', value: Math.round(Math.random() * 1000)},
                            {name: '云南', value: Math.round(Math.random() * 1000)},
                            {name: '辽宁', value: Math.round(Math.random() * 1000)},
                            {name: '黑龙江', value: Math.round(Math.random() * 1000)},
                            {name: '湖南', value: Math.round(Math.random() * 1000)},
                            {name: '安徽', value: Math.round(Math.random() * 1000)},
                            {name: '山东', value: Math.round(Math.random() * 1000)},
                            {name: '新疆', value: Math.round(Math.random() * 1000)},
                            {name: '江苏', value: Math.round(Math.random() * 1000)},
                            {name: '浙江', value: Math.round(Math.random() * 1000)},
                            {name: '江西', value: Math.round(Math.random() * 1000)},
                            {name: '湖北', value: Math.round(Math.random() * 1000)},
                            {name: '广西', value: Math.round(Math.random() * 1000)},
                            {name: '甘肃', value: Math.round(Math.random() * 1000)},
                            {name: '山西', value: Math.round(Math.random() * 1000)},
                            {name: '内蒙古', value: Math.round(Math.random() * 1000)},
                            {name: '陕西', value: Math.round(Math.random() * 1000)},
                            {name: '吉林', value: Math.round(Math.random() * 1000)},
                            {name: '福建', value: Math.round(Math.random() * 1000)},
                            {name: '贵州', value: Math.round(Math.random() * 1000)},
                            {name: '广东', value: Math.round(Math.random() * 1000)},
                            {name: '青海', value: Math.round(Math.random() * 1000)},
                            {name: '西藏', value: Math.round(Math.random() * 1000)},
                            {name: '四川', value: Math.round(Math.random() * 1000)},
                            {name: '宁夏', value: Math.round(Math.random() * 1000)},
                            {name: '海南', value: Math.round(Math.random() * 1000)},
                            {name: '台湾', value: Math.round(Math.random() * 1000)},
                            {name: '香港', value: Math.round(Math.random() * 1000)},
                            {name: '澳门', value: Math.round(Math.random() * 1000)}
                        ]
                    }
                ]
            };
            mapChart.setOption(mapChartOption);

            //环形图表
            let ringChart = echarts.init(document.getElementById('ring-chart'), 'shine');
            let ringChartOption = {
                tooltip: {
                    trigger: 'item',
                    axisPointer: {
                        type: 'shadow'
                    }
                },
                visualMap: {
                    min: 0,
                    max: 100,
                    inRange: {
                        color: ['#224eb1', '#04fccc']
                    },
                    calculable: true,
                    show: false
                },
                series: [{
                    name: '全校',
                    type: 'pie',
                    radius: ['60%', '70%'],
                    center: ['50%', '50%'],
                    minAngle: 0,
                    data: [{
                        value: 70,
                        name: '已报到',
                        label: {
                            normal: {
                                show: true,
                                formatter: '{d}%',
                                textStyle: {
                                    fontSize: 25,
                                    color: '#fff'
                                }
                            }
                        }
                    }, {
                        value: 30,
                        name: '未报到'
                    }],
                    label: {
                        normal: {
                            show: false,
                            position: 'center'
                        }
                    },
                    labelLine: {
                        normal: {
                            show: false
                        },
                        emphasis: {
                            show: false
                        }
                    },
                    itemStyle: {
                        emphasis: {
                            shadowBlur: 10,
                            shadowOffsetX: 0,
                            shadowColor: 'rgba(0, 0, 0, 0.5)'
                        }
                    }
                }]

            };
            ringChart.setOption(ringChartOption);

            //饼状图表
            let pieChart = echarts.init(document.getElementById('pie-chart'), 'shine');
            let pieChartOption = {
                tooltip: {
                    trigger: 'item',
                    axisPointer: {
                        type: 'shadow'
                    }
                },
                label: {
                    normal: {
                        show: true,
                        formatter: '{d}%\n{b}'
                    }
                },
                textStyle: {
                    color: '#fff'
                },
                series: [
                    {
                        name: '访问来源',
                        type: 'pie',
                        radius: '50%',
                        data: [
                            {value: 235, name: '视频广告'},
                            {value: 274, name: '联盟广告'},
                            {value: 310, name: '邮件营销'},
                            {value: 335, name: '直接访问'},
                            {value: 400, name: '搜索引擎'}
                        ]
                    }
                ]
            };
            pieChart.setOption(pieChartOption);

            //折线统计图1
            let base = +new Date(2016, 9, 3);
            let oneDay = 24 * 3600 * 1000;
            let valueBase = Math.random() * 300;
            let data = [];

            for (let i = 1; i < 20; i++) {
                let now = new Date(base += oneDay);
                let dayStr = [now.getFullYear(), now.getMonth() + 1, now.getDate()].join('-');
                valueBase = Math.round((Math.random() - 0.5) * 20 + valueBase);
                valueBase <= 0 && (valueBase = Math.random() * 50);
                data.push([dayStr, valueBase]);
            }

            let lineChart1 = echarts.init(document.getElementById('line-chart-1'), 'shine');
            let lineChartOption1 = {
                animation: true,
                textStyle: {
                    color: '#fff'
                },
                xAxis: {
                    type: 'time',
                    splitLine: {
                        show: false
                    }
                },
                yAxis: {
                    type: 'value',
                    axisLabel: {
                        inside: false,
                        formatter: '{value}\n'
                    },
                    z: 10
                },
                series: [
                    {
                        name: '模拟数据',
                        type: 'line',
                        smooth: false,
                        stack: 'a',
                        symbol: 'none',
                        symbolSize: 5,
                        sampling: 'average',
                        itemStyle: {
                            normal: {
                                color: '#fff'
                            }
                        },
                        areaStyle: {
                            normal: {
                                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                    offset: 0,
                                    color: '#006edd'
                                }, {
                                    offset: 1,
                                    color: 'rgba(0, 0, 0, 0.5)'
                                }])
                            }
                        },
                        data: data//[["2016-10-4", 5], ["2016-10-5", 1], ["2016-10-6", 6]]
                    }

                ]
            };
            lineChart1.setOption(lineChartOption1);

            //折线统计图2
            console.log(data);
            let lineChart2 = echarts.init(document.getElementById('line-chart-2'), 'shine');
            let lineChartOption2 = {
                animation: true,
                tooltip: {
                    trigger: 'item',
                    axisPointer: {
                        type: 'shadow'
                    }
                },
                textStyle: {
                    color: '#224eb1'
                },
                xAxis: {
                    type: 'time',
                    splitLine: {
                        show: false
                    }
                },
                yAxis: {
                    type: 'value',

                    splitLine: {
                        show: false
                    },
                    axisLabel: {
                        inside: false,
                        formatter: '{value}\n'
                    },
                    z: 10
                },
                series: [
                    {
                        name: '模拟数据',
                        type: 'line',
                        smooth: false,
                        stack: 'a',
                        symbol: 'circle',
                        symbolSize: 5,
                        sampling: 'average',
                        itemStyle: {
                            normal: {
                                color: '#006edd'
                            }
                        },
                        areaStyle: {
                            normal: {
                                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                    offset: 0,
                                    color: '#006edd'
                                }, {
                                    offset: 1,
                                    color: 'rgba(0, 0, 0, 0.5)'
                                }])
                            }
                        },
                        data: [["2016-10-4", 5], ["2016-10-5", 1], ["2016-10-6", 6]]
                    }
                ]
            };
            lineChart2.setOption(lineChartOption2);
        }
    }
</script>

<style scoped>
    .content {
        width: 100vw;
        height: 100vh;
        background-image: url("../../assets/xinkong.jpg");
    }

    .main-bg {
        background-color: rgba(24, 28, 75, 0.7);
    }

    .title-div {
        position: relative;
        width: 100%;
        height: 8vh;
        text-align: center;
        vertical-align: middle;
    }

    .middle-div {
        text-align: center;
        width: 100%;
        height: 70vh;
    }

    .left-div {
        display: inline-block;
        width: 12vw;
        height: calc(100% - 20PX);
        vertical-align: top;
        margin: 10PX 0PX 10PX 0PX;
    }

    .left2-div {
        position: relative;
        display: inline-block;
        width: 44vw;
        height: calc(100% - 20PX);
        vertical-align: top;
        margin: 10PX 0PX 10PX 0PX;
    }

    .map {
        width: 100%;
        height: 100%;
    }

    .right-div {
        position: relative;
        display: inline-block;
        width: 16vw;
        height: calc(100% - 20PX);
        vertical-align: top;
        margin: 10PX 0PX 10PX 0PX;
    }

    .right2-div {
        position: relative;
        display: inline-block;
        width: 24vw;
        height: calc(100% - 20PX);
        vertical-align: top;
        margin: 10PX 0PX 10PX 0PX;
    }

    .bottom-div {
        text-align: center;
        width: 100%;
        height: 21vh;
    }

    .bottom-bg {
        border-top: solid 4PX #113158;
    }

    .bottom1-div {
        position: relative;
        display: inline-block;
        width: 12vw;
        height: 100%;
        vertical-align: top;
    }

    .bottom2-div {
        display: inline-block;
        width: 44vw;
        height: 100%;
        vertical-align: top;
    }

    .bottom3-div {
        display: inline-block;
        width: 40.3vw;
        height: 100%;
        vertical-align: top;
    }

    .scroll-bar::-webkit-scrollbar {
        width: 4PX;
        background-color: #3b4b64;
    }

    .scroll-bar::-webkit-scrollbar-thumb {
        background-color: #aae5ff;
    }

    .scroll-bar::-webkit-scrollbar-track {
        -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
        background-color: #3b4b64;
    }

    .title-text {
        color: white;
        line-height: 8vh;
        font-size: 2em;
        display: block;
        font-weight: bold;
    }

    .time-div {
        position: absolute;
        line-height: 8vh;
        top: 0;
        right: 5%;
        color: #1a7fe1;
    }

    .left-div-title {
        color: white;
        font-size: 1.1em;
        margin-top: 10PX;
        font-weight: bold;
        display: block;
        text-align: center;
    }

    .left-div-sub-title {
        color: #224eb1;
        font-size: 0.6em;
        font-weight: bold;
        display: block;
        text-align: center;
    }

    .left-div-content-div {
        height: 90%;
        overflow: auto;
    }

    .p-10 {
        padding: 10PX;
    }

    .mt-10 {
        margin-top: 10PX;
    }

    .tal {
        text-align: left !important;
    }

    .no-text {
        color: #224eb1;
        text-align: left;
    }

    .no-name-text {
        color: white;
        text-align: left;
    }

    .no-progress-bg {
        background-color: #1e2a56;
        width: 100%;
        height: 5PX;
        margin-top: 10PX;
    }

    .no-progress {
        background-color: #224eb1;
        height: 100%;
    }

    .left2-content-div {
        position: absolute;
        top: 10PX;
        left: 10PX;
    }

    .left2-title1 {
        border-left: solid 4PX #224eb1;
        padding-left: 10PX;
    }

    .left2-title2 {
        border-left: solid 4PX #224eb1;
        padding-left: 10PX;
        margin-top: 10PX;
    }

    .left2-title1-label {
        color: #838ce9;
        font-size: 18PX;
        font-weight: bold;
        display: block;
    }

    .left2-title1-num {
        color: white;
        font-size: 24PX;
        font-weight: bold;
        display: inline-block;
    }

    .left2-title1-ren {
        color: #838ce9;
        font-size: 24PX;
        font-weight: bold;
        display: inline-block;
    }

    .left2-title2-label {
        color: #838ce9;
        font-size: 18PX;
        font-weight: bold;
        display: block;
    }

    .left2-title2-num {
        color: white;
        font-size: 24PX;
        font-weight: bold;
        display: block;
    }

    .right-content1 {
        width: 100%;
        height: 48%;
        position: absolute;
        top: 0;
    }

    .right-content1-title-div {
        position: relative;
        padding: 10PX;
    }

    .right-content1-title-area {
        position: absolute;
        top: 10PX;
        left: 10PX;
    }

    .right-content1-title {
        color: white;
        font-size: 1.1em;
        font-weight: bold;
        display: block;
    }

    .right-content1-sub-title {
        color: #224eb1;
        font-size: 0.6em;
        font-weight: bold;
        display: block;
    }

    .right-content1-num-div {
        position: absolute;
        top: 6PX;
        right: 10PX;
    }

    .right-content1-num-text {
        color: white;
        font-size: 2.2em;
    }

    .right-content1-num {
        color: #4dcef6;
        font-size: 2.2em;
    }

    .ring-chart {
        width: 60%;
        height: 76%;
        margin: auto;
    }

    .right-content1-item1-div {
        width: 38%;
        position: absolute;
        bottom: 10PX;
        left: 10PX;
        padding: 10PX;
        text-align: left !important;
    }

    .right-content1-item1-title {
        color: #347ec9;
        font-size: 18PX;
        display: block;
    }

    .right-content1-item1-num {
        color: white;
        font-size: 24PX;
        font-weight: bold;
        display: inline-block;
    }

    .right-content1-item1-wan {
        color: #347ec9;
        font-size: 24PX;
        font-weight: bold;
        display: inline-block;
    }

    .right-content1-item2-div {
        width: 38%;
        position: absolute;
        bottom: 10PX;
        right: 10PX;
        padding: 10PX;
        text-align: left !important;
    }

    .right-content1-item2-title {
        color: #347ec9;
        font-size: 18PX;
        display: block;
    }

    .right-content1-item2-jia {
        color: #ff571a;
        font-size: 24PX;
        font-weight: bold;
        display: inline-block;
    }

    .right-content1-item2-num {
        color: #347ec9;
        font-size: 24PX;
        font-weight: bold;
        display: inline-block;
    }

    .right-content2 {
        width: 100%;
        height: 48%;
        position: absolute;
        bottom: 0;
    }

    .right-content2-content {
        position: relative;
        padding: 10PX;
        display: block;
        height: 100%;
    }

    .right-content2-title-div {
        position: absolute;
        top: 10PX;
        left: 10PX;
    }

    .right-content2-title {
        color: white;
        font-size: 1.1em;
        font-weight: bold;
        display: block;
    }

    .right-content2-sub-title {
        color: #224eb1;
        font-size: 0.6em;
        font-weight: bold;
        display: block;
    }

    .right-content2-num-div {
        position: absolute;
        top: 6PX;
        right: 10PX;
    }

    .right-content2-num-text {
        color: white;
        font-size: 2.2em;
    }

    .right-content2-num {
        color: #4dcef6;
        font-size: 2.2em;
    }

    .right-content2-data-list {
        margin-top: 18%;
        display: block;
        text-align: center;
        height: 76%;
        overflow: auto;
    }

    .right-content2-data-list-item-title {
        display: inline-block;
        font-size: 14PX;
        color: #224eb1;
        width: 10%;
        vertical-align: top;
    }

    .right-content2-data-list-item-progress-bg {
        background-color: #1e2a56;
        width: 80%;
        height: 12PX;
        display: inline-block
    }

    .right-content2-data-list-item-progress {
        background-color: #04fccc;
        height: 100%;
    }

    .right2-content1 {
        width: 100%;
        height: 48%;
        position: absolute;
        top: 0;
        left: 0;
    }

    .right2-content1-div {
        position: relative;
        padding: 10PX;
        display: block;
    }

    .right2-content1-title-div {
        position: absolute;
        top: 10PX;
        left: 10PX;
    }

    .right2-content1-title {
        color: white;
        font-size: 1.1em;
        font-weight: bold;
        display: block;
    }

    .pie-chart {
        width: 100%;
        height: 100%;
    }

    .right2-content2 {
        width: 100%;
        height: 48%;
        position: absolute;
        bottom: 0;
    }

    .right2-content2-div {
        position: relative;
        padding: 10PX;
        display: block;
    }

    .right2-content2-title-div {
        position: absolute;
        top: 10PX;
        left: 10PX;
    }

    .right2-content2-title {
        color: white;
        font-size: 1.1em;
        font-weight: bold;
        display: block;
    }

    .line-chart-1 {
        width: 100%;
        height: 100%;
    }

    .logo {
        position: absolute;
        top: 16%;
        left: 0;
        width: 100%;
        height: auto;
        background-color: white;
    }

    .bottom2-div-title-area {
        position: relative;
        padding: 10PX;
        display: block;
    }

    .bottom2-div-title-div {
        position: absolute;
        top: 10PX;
        left: 10PX;
    }

    .bottom2-div-title {
        color: white;
        font-size: 1.1em;
        font-weight: bold;
        display: block;
    }

    .line-chart-2 {
        width: 100%;
        height: 90%;
    }

    .bottom3-div-title-area {
        position: relative;
        padding: 10PX;
        display: block;
        width: 100%;
    }

    .bottom3-div-title-div {
        position: absolute;
        top: 10PX;
        left: 10PX;
    }

    .bottom3-div-title {
        color: white;
        font-size: 1.1em;
        font-weight: bold;
        display: block;
    }

    .bottom3-div-content {
        width: 100%;
        padding-top: 6%;
        text-align: left !important;
    }

    .bottom3-div-content-item {
        width: 25%;
        border-right: solid 2PX #224eb1;
        padding-right: 2%;
        padding-left: 2%;
        display: inline-block;
        vertical-align: top;
    }

    .bottom3-div-content-item-text {
        color: #224eb1;
        text-align: left;
        display: inline-block;
        font-size: 0.8em;
    }

    .bottom3-div-content-item-num {
        color: #224eb1;
        text-align: right;
        display: inline-block;
        font-size: 1.2em;
        margin-left: 5%
    }

    .mt-20 {
        margin-top: 20PX;
    }
</style>