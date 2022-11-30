<template>
    <!-- <div>Bmap</div> -->
    <div id="container"></div>
</template>

<script>
import { onMounted } from "vue";
export default {
    name: "Bmap",
    setup(props) {
        onMounted(() => {
            var map = new BMapGL.Map("container"); // 创建地图实例
            var point = new BMapGL.Point(116.404, 39.915); // 创建点坐标
            map.centerAndZoom(point, 15); // 初始化地图，设置中心点坐标和地图级别
            map.enableScrollWheelZoom(true); //开启鼠标滚轮缩放
            var scaleCtrl = new BMapGL.ScaleControl(); // 添加比例尺控件
            map.addControl(scaleCtrl);
            var zoomCtrl = new BMapGL.ZoomControl(); // 添加缩放控件
            map.addControl(zoomCtrl);
            var cityCtrl = new BMapGL.CityListControl(); // 添加城市列表控件
            map.addControl(cityCtrl);
            var marker = new BMapGL.Marker(point); // 创建标注
            map.addOverlay(marker); // 将标注添加到地图中
            marker.addEventListener("click", function () {
                alert("您点击了标注");
            });
        });
    },
};
</script>

<style scoped>
#container {
    width: 100%;
    height: 900px;
}
</style>