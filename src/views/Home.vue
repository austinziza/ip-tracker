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

    <div class="container">
    <div  class="row pt-5">
      <div class= "col-xl-6 offset-xl-3 col-lg-6 offset-lg-3 col-md-6 offset-md-3 col-sm-12">
        <div style="background-color: white; border-radius: 10px">
          <div class="row pt-5 pb-5">

            <div class="col-lg-1 col-md-12 col-sm-12">
            </div>

            <div class="col-lg-2 col-md-12 col-sm-12">
              <span class="title">IP ADDRESS</span><br/>
              <h5>{{ip}}</h5>
            </div>

            <div class="col-lg-2 col-md-12 col-sm-12">
              <span class="title">LOCATION</span><br/>
              <h5>California</h5>
            </div>

            <div class="col-lg-2 col-md-12 col-sm-12">
              <span class="title ">TIMEZONE</span><br/>
              <h5>UTC-08:00</h5>
            </div>

            <div class="col-lg-2 col-md-12 col-sm-12">
              <span class="title">ISP</span><br/>
              <h5>Google LLc</h5>
            </div>

            <div class="col-lg-2 col-md-12 col-sm-12">
              <span class="title">STATE</span><br/>
              <h5>New York</h5>
            </div>

            <div class="col-lg-1 col-md-12 col-sm-12">
            </div>

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

h5{
  font-size: 15px;
  font-weight: bolder;
}

.title{
  font-size: 10px;
  font-weight: bold;
}
</style>
