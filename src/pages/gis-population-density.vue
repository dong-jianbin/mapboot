<template>
  <div id="map" style="margin:0 auto;width: 100%;height: 100%;"></div>
</template>

<script>
  import {chinaProvider} from 'leaflet.chinatmsproviders'
  import HeatmapOverlay from 'heatmap.js/plugins/leaflet-heatmap'
  import L from 'leaflet'

  export default {
    name: 'gis-population-density',
    data () {
      return {
        heatmapLayer: null,
        map: null
      }
    },
    mounted () {
      this.initmap()
    },
    methods: {
      initmap: function () {
        let max = 800
        let points = []

        for (let i = 0; i < max; i++) {
          let lat = 43.8 + Math.ceil(Math.random() * 300000) * 0.000001
          let lng = 125.2 + Math.ceil(Math.random() * 300000) * 0.000001
          let count = Math.ceil(Math.random() * 1)
          let point = {
            lat: lat,
            lng: lng,
            count: count
          }
          points.push(point)
          // console.log(point)
        }

        var SimulateData =
          {max: max,
            data: points}

        // 配置
        var cfg = {
          // 热力点半径
          'radius': 0.005,
          // 透明度
          'maxOpacity': 0.8,
          // 随比例尺变化
          'scaleRadius': true,
          'useLocalExtrema': true,
          latField: 'lat',
          lngField: 'lng',
          valueField: 'count'
        }
        this.heatmapLayer = new HeatmapOverlay(cfg)
        // 热力图
        this.heatmapLayer.setData(SimulateData)

        var normalm = L.tileLayer.chinaProvider('GaoDe.Normal.Map', {
          attribution: 'Haut-Gis-Org © 高德地图',
          maxZoom: 18,
          minZoom: 5
        })
        var imgm = L.tileLayer.chinaProvider('GaoDe.Satellite.Map', {
          attribution: 'Haut-Gis-Org © 高德地图',
          maxZoom: 18,
          minZoom: 5
        })
        var imga = L.tileLayer.chinaProvider('GaoDe.Satellite.Annotion', {
          attribution: 'Haut-Gis-Org © 高德地图',
          maxZoom: 18,
          minZoom: 5
        })

        let normal = L.layerGroup([normalm])
        let image = L.layerGroup([imgm, imga])

        // 图层
        let OpenStreetMap = L.tileLayer(
          'http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: 'Haut-Gis-Org © OpenStreetMap'
          }
        )

        var baseLayers = {
          '地图': normal,
          '影像': image,
          'OpenStreetMap': OpenStreetMap
        }

        var map = L.map('map', {
          center: [43.912301, 125.323877],
          zoom: 12,
          layers: [normal],
          zoomControl: false
        })

        let overlays = {
          '人群密集热力图': this.heatmapLayer
        }
        L.control.layers(baseLayers, overlays).addTo(map)
        L.control.zoom({
          zoomInTitle: '放大',
          zoomOutTitle: '缩小'
        }).addTo(map)
      }
    }
  }
</script>

<style scoped>
  /*@import "~leaflet";*/
</style>
