<template>
  <div class="about">
    <div id="map" style="height: 1000px"></div>
    <div v-if="showPopup" class="popup">
      <p>{{ popupContent }}</p>
      <button @click="showPopup = false">关闭</button>
    </div>
  </div>
</template>

<script>
import L from "leaflet";
import "leaflet/dist/leaflet.css";

export default {
  name: "AboutView",
  data() {
    return {
      map: null,
      showPopup: false,
      popupContent: "",
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      // 初始化地图并设置中心点和缩放级别
      this.map = L.map("map").setView([-36.866612, 174.766033], 13);
      L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        maxZoom: 19,
        attribution: "© OpenStreetMap contributors",
      }).addTo(this.map);

      // 添加一个示例标记点
      const marker = L.marker([-36.866612, 174.766033]).addTo(this.map);
      marker.on("click", () => {
        // 点击标记点时显示弹窗
        this.popupContent = "未来几天的空气质量预测...";
        this.showPopup = true;
      });
    },
  },
};
</script>

<style>
/* 导入 Leaflet CSS */
@import "~leaflet/dist/leaflet.css";

/* 弹窗样式 */
.popup {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  z-index: 1000;
}
</style>
