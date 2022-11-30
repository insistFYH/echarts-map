<template>
    <div id="container"></div>
</template>

<script>
import AMapLoader from "@amap/amap-jsapi-loader";
import { shallowRef, onMounted } from "vue";
export default {
    name: "Map",
    setup(props) {
        let map = shallowRef(null);
        function showInfoM(e) {
            var text =
                "您在 [ " +
                e.lnglat.getLng() +
                "," +
                e.lnglat.getLat() +
                " ] 的位置点击了marker！";
            alert(text);
        }
        function initMap() {
            AMapLoader.load({
                key: "1e63a4db957a624a12ea1f9450cb201d", // 申请好的Web端开发者Key，首次调用 load 时必填
                version: "2.0", // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
                plugins: [""], // 需要使用的的插件列表，如比例尺'AMap.Scale'等
            })
                .then((AMap) => {
                    map = new AMap.Map("container", {
                        //设置地图容器id
                        viewMode: "3D", //是否为3D地图模式
                        zoom: 11, //初始化地图级别
                        center: [118.767413, 32.041544], //初始化地图中心点位置
                    });
                    // 创建一个 Marker 实例：
                    var marker = new AMap.Marker({
                        position: new AMap.LngLat(118.767413, 32.041544), // 经纬度对象，也可以是经纬度构成的一维数组[116.39, 39.9]
                        title: "南京",
                    });
                    map.add(marker);
                    marker.on("click", showInfoM);
                })
                .catch((e) => {
                    console.log(e);
                });
        }
        onMounted(() => {
            initMap();
        });
        return {
            map,
        };
    },
};
</script>

<style  scoped>
#container {
    padding: 0px;
    margin: 0px;
    width: 100%;
    height: 900px;
}
</style>