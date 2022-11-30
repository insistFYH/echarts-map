<template>
    <!-- <div>Bmap</div> -->
    <div id="container"></div>
</template>

<script>
import { onMounted } from "vue";
export default {
    name: "Tmap",
    setup(props) {
        function init() {
            // var myLatlng = new qq.maps.LatLng(32.041544, 118.767413);
            // var myOptions = {
            //     zoom: 11,
            //     center: myLatlng,
            //     mapTypeId: qq.maps.MapTypeId.ROADMAP,
            // };
            // var map = new qq.maps.Map(
            //     document.getElementById("container"),
            //     myOptions
            // );
            var center = new qq.maps.LatLng(32.041544, 118.767413);
            var map = new qq.maps.Map(document.getElementById("container"), {
                center: center,
                zoom: 13,
            });
            var marker = new qq.maps.Marker({
                position: center,
                map: map,
            });
            qq.maps.event.addListener(marker, "click", function () {
                alert("点击标注");
            });
        }

        function loadScript() {
            init();
        }
        onMounted(() => {
            loadScript();
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