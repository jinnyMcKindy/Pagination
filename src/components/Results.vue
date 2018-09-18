<template>
    <div class="c2c-item">
        <div class='srch-title'>
            {{title}}
        </div>
        <div class='srch-description'>
            {{description}}
        </div>
        <div class='srch-url'>
            <a :href="url">{{url}}</a>
        </div>
    </div>
</template>

<script>
export default { 
  name : 'results',
  props : ["title", "description", "url"],
};
</script>