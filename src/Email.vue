<template>
    <v-ons-page>
        <custom-toolbar :back-label="'Home'">Email</custom-toolbar>
    </v-ons-page>
</template>

<script>
  import customToolbar from './CustomToolbar';
  export default {
    methods: {
      pop() {
        this.pageStack.pop();
      }
    },
    props: ['pageStack'],
    components: { customToolbar }
  }
</script>
