<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>ZipCode App</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ZipSearch v-on:get-zip="getZipInfo"/>
      <ZipInfo v-bind:info="info"/>
    </ion-content>
  </div>
</template>

<script>
// @ is an alias to /src
import ZipSearch from '../components/ZipSearch'
import ZipInfo from '../components/ZipInfo'

export default {
  name: 'home',
  components: { ZipSearch, ZipInfo },
  data(){
    return {
      info: null
    }
  },
  methods: {
    async getZipInfo(zip){
      const res = await fetch(`https://api.zippopotam.us/us/${zip}`);
      //check status before JSON conversion
      if(res.status == 404){
        this.showAlert();
      }
      this.info = await res.json();
    },
    showAlert(){
            return this.$ionic.alertController
            .create({
                header: "Not Valid",
                message: "Please enter a valid US Zip Code...",
                buttons: ["OK"]
            })
            .then(a => a.present())
        }
  }
}
</script>
