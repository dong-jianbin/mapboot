<template>
  <div id="map" style="margin:0 auto;width: 100%;height: 100%"></div>
</template>

<script>
    import {chinaProvider} from 'leaflet.chinatmsproviders'
    import L from 'leaflet'
    import 'proj4leaflet'
    import 'proj4'
    export default {
      name: 'dev-mastre-map',
      data () {
        return {
          map: null
        }
      },
      mounted () {
        this.initmap()
      },
      methods: {
        initmap: function () {
          let normalMap = L.tileLayer.chinaProvider('Baidu.Normal.Map', {
            maxZoom: 18,
            minZoom: 5
          })
          let satelliteMap = L.tileLayer.chinaProvider('Baidu.Satellite.Map', {
            maxZoom: 18,
            minZoom: 5
          })
          let annotionMap = L.tileLayer.chinaProvider('Baidu.Satellite.Annotion', {
            maxZoom: 18,
            minZoom: 5
          })
          let Baiduimage = L.layerGroup([satelliteMap, annotionMap])

          var baseLayers = {
            '地图': normalMap,
            '影像': Baiduimage
          }

          // var overlayLayers = {
          //   '标注': annotionMap
          // }


          var crs = new L.Proj.CRS('EPSG:900913',
            '+proj=merc +a=6378206 +b=6356584.314245179 +lat_ts=0.0 +lon_0=0.0 +x_0=0 +y_0=0 +k=1.0 +units=m +nadgrids=@null +wktext  +no_defs',
            {
              resolutions: function () {
                var level = 19
                var res = []
                res[0] = Math.pow(2, 18)
                for (var i = 1; i < level; i++) {
                  res[i] = Math.pow(2, (18 - i))
                }
                return res
              }(),
              origin: [0, 0],
              bounds: L.bounds([20037508.342789244, 0], [0, 20037508.342789244])
            })

          var map = L.map('map', {
            crs: crs,
            minZoom: 3,
            maxZoom: 18,
            attributionControl: false,
            center: [43.912301, 125.323877],
            zoom: 12,
            zoomControl: false,
            layers: [normalMap]
          })

          L.control.layers(baseLayers, null).addTo(map)
          L.control.zoom({
            zoomInTitle: '放大',
            zoomOutTitle: '缩小'
          }).addTo(map)
        }
      }
    }
</script>
<style scoped>

</style>
