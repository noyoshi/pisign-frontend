<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12" class="pa-0">
        <p class="mb-0">{{ time }}</p>
      </v-col>
    </v-row>
    <v-row class="text-center">
      <v-col cols="12" class="pa-0">
        <p class="mb-0">{{ date }}</p>
      </v-col>
    </v-row>
  </v-container>
</template>

<style>
  .display-datetime {
    overflow-wrap: break-word;
  }
</style>
<script>
export default {
  name: 'TimeWidget',
  data: function(){
    return {
      date: "",
      time: ""
    }
  },
  created() {
    this.getTime();
    setInterval(this.getTime, 1000);
  },
  methods: {
    getTime: function(){
      const today = new Date();
      this.date = (today.getMonth()+1) + '-' + today.getDate() + "-" + today.getFullYear();
      const hour = today.getHours();
      this.time = "";
      var suffix = "";
      if (hour < 12){
        suffix = " AM";
      } else {
        suffix = " PM";
      }
      // Changing the hour of the 24 hour time
      if (hour == 0){
        this.time = "12";
      } else if (hour < 13){
        this.time = hour;
      } else {
        this.time = (hour-12);
      }
      this.time += ":" + this.pad(today.getMinutes(),2) + ":" + this.pad(today.getSeconds(),2) + suffix;
    },
    pad: function (n, width) {
      n = n + '';
      return n.length >= width ? n : new Array(width - n.length + 1).join('0') + n;
    }
  }
}
</script>
