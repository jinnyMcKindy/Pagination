<template>
  <div class="c2c-dot" v-on:click="$emit('click-dots', value)" v-if="Max">...</div>
</template>
<script>
  export default {
    name : 'dot-component',
    props : ["Max", "value"],
  };
</script>

