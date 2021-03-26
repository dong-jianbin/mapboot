<template>
  <div id="map" style="margin:0 auto;width: 100%;height: 100%"></div>
</template>

<script>
    import {chinaProvider} from 'leaflet.chinatmsproviders'
    import 'leaflet.markercluster'
    import 'leaflet-draw'
    import L from 'leaflet'
    export default {
      name: 'gis-geo-edit',
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
          /**
           * Esri地图
           */
          let EsriWorldImagery = L.tileLayer('http://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
            attribution: 'Tiles &copy; Esri &mdash; Source: Esri, i-cubed, USDA, USGS, ' +
              'AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-EGP, and the GIS User Community'
          })

          let EsriDarkGreyCanvas = L.tileLayer(
            'http://{s}.sm.mapstack.stamen.com/' +
            '(toner-lite,$fff[difference],$fff[@23],$fff[hsl-saturation@20])/' +
            '{z}/{x}/{y}.png',
            {
              attribution: 'Tiles &copy; Esri &mdash; Esri, DeLorme, NAVTEQ, TomTom, Intermap, iPC, USGS, FAO, ' +
                'NPS, NRCAN, GeoBase, Kadaster NL, Ordnance Survey, Esri Japan, METI, Esri China (Hong Kong), and the GIS User Community'
            }
          )
          /**
           * 智图地图内容
           */
          let normalm1 = L.tileLayer.chinaProvider('Geoq.Normal.Map', {
            attribution: 'Asiainfo-Gis-Open © 智图地图'
          })
          // let normalm2 = L.tileLayer.chinaProvider('Geoq.Normal.Color', {
          //   attribution: 'Asiainfo-Gis-Open © 智图地图'
          // })
          let normalm3 = L.tileLayer.chinaProvider('Geoq.Normal.PurplishBlue', {
            attribution: 'Asiainfo-Gis-Open © 智图地图'
          })
          let normalm4 = L.tileLayer.chinaProvider('Geoq.Normal.Gray', {
            attribution: 'Asiainfo-Gis-Open © 智图地图'
          })
          let normalm5 = L.tileLayer.chinaProvider('Geoq.Normal.Warm', {
            attribution: 'Asiainfo-Gis-Open © 智图地图'
          })
          // let normalm6 = L.tileLayer.chinaProvider('Geoq.Normal.Cold', {
          //   attribution: 'Asiainfo-Gis-Open © 智图地图'
          // })
          /**
           * 天地图内容
           */
          let normalm = L.tileLayer.chinaProvider('TianDiTu.Normal.Map', {
            attribution: 'Asiainfo-Gis-Open © 天地图',
            key: 'dbeb4d20be0faecb77c6bd90f075f69d'
          })
          let normala = L.tileLayer.chinaProvider('TianDiTu.Normal.Annotion', {
            attribution: 'Asiainfo-Gis-Open © 天地图',
            key: 'dbeb4d20be0faecb77c6bd90f075f69d'
          })
          let imgm = L.tileLayer.chinaProvider('TianDiTu.Satellite.Map', {
            key: 'dbeb4d20be0faecb77c6bd90f075f69d',
            attribution: 'Asiainfo-Gis-Open © 天地图'
          })
          let imga = L.tileLayer.chinaProvider('TianDiTu.Satellite.Annotion', {
            attribution: 'Asiainfo-Gis-Open © 天地图',
            key: 'dbeb4d20be0faecb77c6bd90f075f69d'
          })
          let normal = L.layerGroup([normalm, normala])
          let image = L.layerGroup([imgm, imga])
          /**
           * 谷歌
           */
          let normalMap = L.tileLayer.chinaProvider('Google.Normal.Map', {
            attribution: 'Asiainfo-Gis-Open © Google Map'
          })
          let satelliteMap = L.tileLayer.chinaProvider('Google.Satellite.Map', {
            attribution: 'Asiainfo-Gis-Open © Google Map'
          })
          /**
           * 高德地图
           */
          let Gaode = L.tileLayer.chinaProvider('GaoDe.Normal.Map', {
            attribution: 'Asiainfo-Gis-Open © AMap'
          })
          let Gaodimgem = L.tileLayer.chinaProvider('GaoDe.Satellite.Map', {
            attribution: 'Asiainfo-Gis-Open © AMap'
          })
          let Gaodimga = L.tileLayer.chinaProvider('GaoDe.Satellite.Annotion', {
            attribution: 'Asiainfo-Gis-Open © AMap'
          })
          let OpenStreetMap = L.tileLayer(
            'http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
              attribution: 'Asiainfo-Gis-Open © OpenStreetMap'
            }
          )
          let MapBox =
            L.tileLayer(
              'https://api.mapbox.com/styles/v1/kengqiangxia/cj5jbah540hlj2rpgh3xptiek/tiles/256/{z}/{x}/{y}?access_token=pk.eyJ1Ijoia2VuZ3FpYW5neGlhIiwiYSI6ImNqNWpiMWZ5ZTIxYzgyd3BrYTN2NDN5aXEifQ.bqY03lR_2LZ0fttPOJ4jyw', {
                attribution: 'Asiainfo-Gis-Open © <a href="http://mapbox.com">Mapbox</a>'
              }
            )

          let Gaodimage = L.layerGroup([Gaodimgem, Gaodimga])
          let baseLayers = {
            'Esri卫星图': EsriWorldImagery,
            'Esri-灰白': EsriDarkGreyCanvas,
            '智图地图': normalm1,
            '智图午夜蓝': normalm3,
            '智图灰色': normalm4,
            '智图暖色': normalm5,
            '天地图': normal,
            '天地图影像': image,
            '谷歌地图': normalMap,
            '谷歌影像': satelliteMap,
            '高德地图': Gaode,
            '高德影像': Gaodimage,
            'OpenStreetMap': OpenStreetMap,
            'MapBox': MapBox
          }
          this.map = L.map('map', {
            center: [43.912301, 125.323877],
            zoom: 12,
            layers: [normalm1],
            zoomControl: false
          })

          let drawnItems = L.featureGroup().addTo(this.map)

          L.control.layers(baseLayers, {'drawlayer': drawnItems}).addTo(this.map)

          L.control.zoom({
            zoomInTitle: '放大',
            zoomOutTitle: '缩小'
          }).addTo(this.map)

          this.map.addControl(new L.Control.Draw({
            edit: {
              featureGroup: drawnItems,
              poly: {
                allowIntersection: false
              }
            },
            draw: {
              polygon: {
                allowIntersection: false,
                showArea: true
              }
            },
            position: 'bottomright'
          }))

          // Truncate value based on number of decimals
          var _round = function (num, len) {
            return Math.round(num * (Math.pow(10, len))) / (Math.pow(10, len))
          }
          // Helper method to format LatLng object (x.xxxxxx, y.yyyyyy)
          var strLatLng = function (latlng) {
            return '(' + _round(latlng.lat, 6) + ', ' + _round(latlng.lng, 6) + ')'
          }

          // Generate popup content based on layer type
          // - Returns HTML string, or null if unknown object
          var getPopupContent = function (layer) {
            // Marker - add lat/long
            if (layer instanceof L.Marker || layer instanceof L.CircleMarker) {
              return strLatLng(layer.getLatLng())
            // Circle - lat/long, radius
            } else if (layer instanceof L.Circle) {
              let center = layer.getLatLng()
              let radius = layer.getRadius()
              return 'Center: ' + strLatLng(center) + '<br />' + 'Radius: ' + _round(radius, 2) + ' m'
            // Rectangle/Polygon - area
            } else if (layer instanceof L.Polygon) {
              let latlngs = layer._defaultShape ? layer._defaultShape() : layer.getLatLngs()
              let area = L.GeometryUtil.geodesicArea(latlngs)
              return 'Area: ' + L.GeometryUtil.readableArea(area, true)
            // Polyline - distance
            } else if (layer instanceof L.Polyline) {
              let latlngs = layer._defaultShape ? layer._defaultShape() : layer.getLatLngs()
              let distance = 0
              if (latlngs.length < 2) {
                return 'Distance: N/A'
              } else {
                for (var i = 0; i < latlngs.length - 1; i++) {
                  distance += latlngs[i].distanceTo(latlngs[i + 1])
                }
                return 'Distance: ' + _round(distance, 2) + ' m'
              }
            }
            return null
          }

          // Object created - bind popup to layer, add to feature group
          this.map.on(L.Draw.Event.CREATED, function (event) {
            var layer = event.layer
            var content = getPopupContent(layer)
            if (content !== null) {
              layer.bindPopup(content)
            }
            drawnItems.addLayer(layer)
          })

          // Object(s) edited - update popups
          this.map.on(L.Draw.Event.EDITED, function (event) {
            let layers = event.layers
            let content = null
            layers.eachLayer(function (layer) {
              content = getPopupContent(layer)
              if (content !== null) {
                layer.setPopupContent(content)
              }
            })
          })

          // this.baseLayer.addTo(this.map)
          // L.control.scale({ maxWidth: 200, metric: true, imperial: false }).addTo(this.map)
          // use event
          // let mypop = L.popup()
          // this.map.on('click', function (e) {
          //   let content = '你临幸了这个点：</br>'
          //   content += e.latlng.toString()
          //   console.log(content)
          //   mypop.setLatLng(e.latlng)
          //     .setContent(content)
          //     // .openOn(this.map)
          //     // .addTo(this.map)
          // })
          // mypop.addTo(this.map)
        }
      }
    }
</script>
<style scoped>

</style>
