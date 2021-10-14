<template>
  <div class="text-center">
    <h2 class="text-3xl font-bold my-5">{{ title }}</h2>
    <div class="text-2xl mt-4 mb-10 font-medium ">{{ timesstamp }}</div>
  </div>
</template>

<script>
import moment from "moment"
export default {
  name: "DataTitle",
  props: ["title", "date"],
  computed:{
      timesstamp: function(){
          return moment(this.date).format("MMMM Do, YYYY")
      }
  }
};
</script>
