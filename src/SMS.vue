<template>
  <v-ons-page>
    <div class="sms-page">
      <custom-toolbar :back-label="'Home'">SMS</custom-toolbar>
      <input class="sms sms-mobile" v-model="numberTxt" placeholder="Enter mobile number" value="" type="tel" />
      <textarea class="sms sms-massage" v-model="messageTxt" placeholder="Enter message"></textarea>
      <v-ons-button class="sms sms-send" @click="sendSms">Send SMS</v-ons-button>
    </div>
  </v-ons-page>
</template>

<script>
  import customToolbar from './CustomToolbar';

  export default {
    data(){
      return {
        numberTxt:'',
        messageTxt:''
      }
    },
    methods: {
      pop() {
        this.pageStack.pop();
      },
      sendSms: function() {
        var number = this.numberTxt.toString(); /* iOS: ensure number is actually a string */
        var message = this.messageTxt
        console.log("number=" + number + ", message= " + message);

        //simple validation for now
        if(number === '' || message === '') return;

        //CONFIGURATION
        var options = {
          replaceLineBreaks: false, // true to replace \n by a new line, false by default
          android: {
            intent: 'INTENT'  // send SMS with the native android SMS messaging
            //intent: '' // send SMS without open any other app
          }
        };

        var success = function () { alert('Message sent successfully'); };
        var error = function (e) { alert('Message Failed:' + e); };
        sms.send(number, message, options, success, error);
      }
    },
    props: ['pageStack'],
    components: { customToolbar }
  }
</script>
