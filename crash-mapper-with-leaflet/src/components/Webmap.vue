<template>
<div id="map">
  <l-map :zoom="16" :minzoom="16" :center="center">
    <l-tile-layer :url="url"></l-tile-layer>
    <l-geo-json :geojson="geojson"></l-geo-json>
  </l-map>
  </div>
</template>

<script>
import {LMap, LTileLayer, LGeoJson} from 'vue2-leaflet';
//var crashCartoAPI = "https://phl.carto.com/api/v2/sql?q=select%20json_build_object(%27type%27,%20%27FeatureCollection%27,%27features%27,%20json_agg(json_build_object(%27type%27,%20%27Feature%27,%20%27properties%27,%20json_build_object(%27crn%27,crn,%27year%27,crash_year,%27maxSeverity%27,max_severity_level)%20,%27geometry%27%20,%20ST_AsGeoJSON(the_geom)::json)))%20AS%20crashdata%20FROM%20crash_data_collision_crash_2013_2017_vz"

export default {
  name: "Webmap",
  components: {
    LMap,
    LTileLayer,
    LGeoJson
  },
  data () {
    return {
      url: 'https://api.mapbox.com/styles/v1/mapbox/light-v9/tiles/{z}/{x}/{y}?access_token=pk.eyJ1IjoiYWtzaGF5N2luMiIsImEiOiJjam1xY3dwd24xb2w0M3BtajloNm01ZnZ1In0.lN36aIIC81PO2KGqyaoB-A',
      center: [ 39.9636, -75.1652], // starting position [lng, lat]
      zoom: 16, // starting zoom
      minzoom: 16
    };
  },
  async created () {
    const response = await fetch('https://services.arcgis.com/fLeGjb7u4uXqeF9q/ArcGIS/rest/services/Street_Centerline/FeatureServer/0/query?where=1%3D1&objectIds=&time=&geometry=%7B+%22x%22%3A+%22-75.1652%22+%2C%22y%22%3A+%2239.9636%22%7D&geometryType=esriGeometryPoint&inSR=4326&spatialRel=esriSpatialRelIntersects&resultType=standard&distance=1500&units=esriSRUnit_Meter&returnGeodetic=true&outFields=SEG_ID%2C+ST_NAME&returnGeometry=true&featureEncoding=esriDefault&multipatchOption=xyFootprint&maxAllowableOffset=&geometryPrecision=&outSR=4326&datumTransformation=&applyVCSProjection=false&returnIdsOnly=false&returnUniqueIdsOnly=false&returnCountOnly=false&returnExtentOnly=false&returnQueryGeometry=false&returnDistinctValues=false&cacheHint=false&orderByFields=&groupByFieldsForStatistics=&outStatistics=&having=&resultOffset=&resultRecordCount=&returnZ=false&returnM=false&returnExceededLimitFeatures=true&quantizationParameters=&sqlFormat=none&f=pgeojson&token=');
    this.geojson = await response.json();
  }
}
</script>