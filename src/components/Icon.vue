<template>
  <span :class="[`icon iconfont ${type}`]" @click='handleClick'></span>
</template>

<script>
export default {
  props:['type','onClick'],
  methods: {
    handleClick(){
      this.$emit('onclick')
    }
  },
}
</script>

<style>

</style>