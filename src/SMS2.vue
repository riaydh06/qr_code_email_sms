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

        if(number === '' || message === '') return;

        var success = function () { alert('Message sent successfully'); };
        var error = function (e) { alert('Message Failed:' + e); };
        if(SMS) {
          SMS.sendSMS(number, message, success, error)
        };
      }
    },
    props: ['pageStack'],
    components: { customToolbar }
  }
</script>
