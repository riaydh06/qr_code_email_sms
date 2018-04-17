<template>
  <v-ons-page>
      <div class="home-page service-list">
          <custom-toolbar>HOME</custom-toolbar>
          <v-ons-button class="service-list-element service-list-element-1" @click="qrcode">Scan Qrcode</v-ons-button>
          <!--<v-ons-button class="service-list-element" @click="sms">SMS</v-ons-button>-->
          <v-ons-button class="service-list-element" @click="sms2">SMS</v-ons-button>
          <v-ons-button class="service-list-element" @click="Email">Email</v-ons-button>
      </div>
  </v-ons-page>
</template>

<script>
  import customToolbar from './CustomToolbar';
  import SMS from './SMS';
  import SMS2 from './SMS2';
  import Email from './Email';
  export default {
     methods: {
       pop(){
         this.pageStack.pop();
       },
       sms() {
         this.pageStack.push(SMS);
       },
       sms2() {
         this.pageStack.push(SMS2);
       },
       Email() {
         this.pageStack.push(Email);
       },
       qrcode(){
         cordova.plugins.barcodeScanner.scan(
           function (result) {
             alert("A barcode has been scanned \n" +
               "Result: " + result.text + "\n" +
               "Format: " + result.format + "\n" +
               "Cancelled: " + result.cancelled);
           },
           function (error) {
             alert("Scanning failed: " + error);
           }
         );
       }
     },
     props: ['pageStack'],
     components: { customToolbar }
  }
</script>
