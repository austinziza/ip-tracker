<template>
  <div class="container">
    <div class="row pt-5 pb-5">
      <div class="col-xl-6 offset-xl-3 col-lg-6 offset-lg-3 col-md-6 offset-md-3 col-sm-12 position-relative">
        <label for="validationTooltipUsername" class="form-label" style="font-size: 25px; color: white;">IP Address
          Tracker</label>
        <div class="input-group">
          <input type="text" v-model="ip" class="form-control" id="validationTooltipUsername"
                 aria-describedby="validationTooltipUsernamePrepend">
          <span style="background-color: #000000; border: black" class="input-group-text"
                id="validationTooltipUsernamePrepend"><i class="fa fa-chevron-right" aria-hidden="true"></i></span>
        </div>
      </div>
    </div>

    <div class="container">
      <div class="row pt-5">
        <div class="col-xl-6 offset-xl-3 col-lg-6 offset-lg-3 col-md-12 col-sm-12">
          <div style="background-color: white; border-radius: 10px">
            <div class="row pt-5 pb-5">

              <div class="col-lg-1 col-md-2 col-sm-12">
              </div>

              <div class="col-lg-2 col-md-2 col-sm-12">
                <span class="title">IP ADDRESS</span><br/>
                <h5>{{ ip }}</h5>
              </div>

              <div class="col-lg-2 col-md-2 col-sm-12">
                <span class="title">LOCATION</span><br/>
                <h5>California</h5>
              </div>

              <div class="col-lg-2 col-md-2 col-sm-12">
                <span class="title ">TIMEZONE</span><br/>
                <h5>UTC-08:00</h5>
              </div>

              <div class="col-lg-2 col-md-2 col-sm-12">
                <span class="title">ISP</span><br/>
                <h5>Google LLc</h5>
              </div>

              <div class="col-lg-2 col-md-2 col-sm-12">
                <span class="title">STATE</span><br/>
                <h5>New York</h5>
              </div>

              <div class="col-lg-1 col-md-2 col-sm-12">
              </div>

            </div>
          </div>

        </div>
      </div>
    </div>

  </div>

  <div id="map" style=" width: 100%; height: 800px;"></div>
</template>

<script>
import {statesData} from "../util/statesData";

export default {
  name: 'Home',
  data() {
    return {
      ip: '8.8.8.8',
      map: null,
      geojson: null,
       info : window.L.control(),
       legend: window.L.control({position: 'bottomright'})
    }
  },
  methods: {
     getColor(d) {
  return d > 1000 ? '#800026' :
      d > 500  ? '#BD0026' :
          d > 200  ? '#E31A1C' :
              d > 100  ? '#FC4E2A' :
                  d > 50   ? '#FD8D3C' :
                      d > 20   ? '#FEB24C' :
                          d > 10   ? '#FED976' :
                              '#FFEDA0';
},

 style(feature) {
  return {
    fillColor: this.getColor(feature.properties.density),
    weight: 2,
    opacity: 1,
    color: 'white',
    dashArray: '3',
    fillOpacity: 0.7
  };
},

 highlightFeature(e) {
  var layer = e.target;

  layer.setStyle({
    weight: 5,
    color: '#666',
    dashArray: '',
    fillOpacity: 0.7
  });

  if (!window.L.Browser.ie && !window.L.Browser.opera && !window.L.Browser.edge) {
    layer.bringToFront();
  }
   this.info.update(layer.feature.properties);
},

 resetHighlight(e) {
  this.geojson.resetStyle(e.target);
   this.info.update();
},

    zoomToFeature(e) {
  this.map.fitBounds(e.target.getBounds());
},

 onEachFeature(feature, layer) {
  layer.on({
    mouseover: this.highlightFeature,
    mouseout: this.resetHighlight,
    click: this.zoomToFeature
  });
}

  },
  mounted() {
    var mapboxAccessToken = process.env.VUE_APP_ACCESS_TOKEN;
    this.map = window.L.map('map').setView([37.8, -96], 4);

    window.L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=' + mapboxAccessToken, {
      id: 'mapbox/light-v9',
      attribution: '',
      tileSize: 512,
      zoomOffset: -1
    }).addTo(this.map);

    this.geojson = window.L.geoJson(statesData, {
      style: this.style,
      onEachFeature: this.onEachFeature
    }).addTo(this.map);



    this.info.onAdd = function () {
      this._div = window.L.DomUtil.create('div', 'info'); // create a div with a class "info"
      this.update();
      return this._div;
    };

// method that we will use to update the control based on feature properties passed
    this.info.update = function (props) {
      this._div.innerHTML = '<h4>US Population Density</h4>' +  (props ?
          '<b>' + props.name + '</b><br />' + props.density + ' people / mi<sup>2</sup>'
          : 'Hover over a state');
    };

    this.info.addTo(this.map);






    this.legend.onAdd =  () => {

      var div = window.L.DomUtil.create('div', 'info legend'),
          grades = [0, 10, 20, 50, 100, 200, 500, 1000];

      // loop through our density intervals and generate a label with a colored square for each interval
      for (var i = 0; i < grades.length; i++) {
        div.innerHTML +=
            '<i style="background:' + this.getColor(grades[i] + 1) + '"></i> ' +
            grades[i] + (grades[i + 1] ? '&ndash;' + grades[i + 1] + '<br>' : '+');
      }

      return div;
    };

    this.legend.addTo(this.map);
  }

}
</script>

<style>
.fa {
  color: #ffffff;
}

.input-group-text:hover {
  cursor: pointer;
}

h5 {
  font-size: 15px;
  font-weight: bolder;
}

.title {
  font-size: 10px;
  font-weight: bold;
}


.info {
  padding: 6px 8px;
  font: 14px/16px Arial, Helvetica, sans-serif;
  background: white;
  background: rgba(255,255,255,0.8);
  box-shadow: 0 0 15px rgba(0,0,0,0.2);
  border-radius: 5px;
}
.info h4 {
  margin: 0 0 5px;
  color: #777;
}

.legend {
  line-height: 18px;
  color: #555;
}
.legend i {
  width: 18px;
  height: 18px;
  float: left;
  margin-right: 8px;
  opacity: 0.7;
}
</style>
