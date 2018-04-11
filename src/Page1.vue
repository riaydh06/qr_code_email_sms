<template>
  <v-ons-page>
    <custom-toolbar>Page 1</custom-toolbar>
    <p style="text-align: center">
      This is the first page
      <v-ons-button @click="push">Push Page 2</v-ons-button>
    </p>
      <v-ons-button @click="qrcode">Push Page 2</v-ons-button>
  </v-ons-page>
</template>

<script>
  import customToolbar from './CustomToolbar';
  import page2 from './Page2';
  export default {
     methods: {
       pop(){
         this.pageStack.pop();
       },
       push() {
         this.pageStack.push(page2);
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
