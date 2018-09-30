<template>
  <div class="c2c-dot" v-on:click="$emit('click-dots', value)" v-if="Max"><div class="dot-inner">{{icon}}</div></div>
</template>
<script>
  export default {
    name : 'dot-component',
    props : ["Max", "value", "icon"],
  };
</script>
<style>
  .dot-inner {
    transform: translateY(50%);
  };
</style>
