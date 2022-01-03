<template>
  <div class="flex justify-center">
    <button class="border rounded-xl bg-indigo-300 px-40 py-2.5"  @click="clickButton">{{labelButton}}</button>
  </div>
</template>

<script>
export default {
  props:{
    labelButton:{
      type:String,
      default:""
    },
  },
  methods:{
    clickButton(){
      this.$emit("click")
    }
  }

}
</script>

<style>

</style>