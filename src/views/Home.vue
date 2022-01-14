<template>
  <div class="container">
  <div  class="row pt-5 pb-5">
    <div class= "col-xl-6 offset-xl-3 col-lg-6 offset-lg-3 col-md-6 offset-md-3 col-sm-12 position-relative">
      <label for="validationTooltipUsername" class="form-label" style="font-size: 25px; color: white;">IP Address Tracker</label>
      <div class="input-group">
        <input type="text" v-model="ip" class="form-control" id="validationTooltipUsername" aria-describedby="validationTooltipUsernamePrepend">
        <span style="background-color: #000000; border: black" class="input-group-text" id="validationTooltipUsernamePrepend"><i class="fa fa-chevron-right" aria-hidden="true"></i></span>
      </div>
    </div>
  </div>

    <div  class="row pt-5 ipDetails">
      <div class= "col-xl-6 offset-xl-3 col-lg-6 offset-lg-3 col-md-6 offset-md-3 col-sm-12 position-relative">
        <div style="background-color: white; border-radius: 10px">
          <div class="row pt-5 pb-5">
            <div class="col-lg-3 col-md-12 col-sm-12">
              <span class="title text-start">IP ADDRESS</span><br/>
              <h4>{{ip}}</h4>
            </div>

            <div class="col-lg-3 col-md-12 col-sm-12">
              <span class="title text-start">LOCATION</span><br/>
              <h4>California</h4>
            </div>

            <div class="col-lg-3 col-md-12 col-sm-12">
              <span class="title text-start">TIMEZONE</span><br/>
              <h4>UTC-08:00</h4>
            </div>

            <div class="col-lg-3 col-md-12 col-sm-12">
              <span class="title float-start col-12">ISP</span><br/>
              <h4 class="col-12">Google LLc</h4>
            </div>

          </div>

        </div>
      </div>
      </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  data(){
    return{
      ip: '8.8.8.8'
    }
  },
}
</script>

<style scoped>
.fa{
  color: #ffffff;
}

.input-group-text:hover{
  cursor: pointer;
}

h4{
  font-weight: bold;
}

.title{
  font-size: 10px;
  font-weight: bold;
}
/*

.ipDetails{
  position: fixed;
  z-index: 300000;
  width: 100%;
  left: 0 !important;
  top: 150px;
  margin-right: 0px!important;
}
*/
</style>
