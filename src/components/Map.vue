<template>
  <div class="map">
    <iframe id="iframe" src="https://map.baidu.com/"></iframe>
  </div>
</template>

<script>
  export default {
    name: 'Map',
    props: {},
    created() {

    },
    methods: {}
  }
</script>

<style scoped>
  .map {
    width: 100%;
    min-height: 100%;
    background: #fff;
  }

  iframe {
    display: block;
    width: 100%;
    min-height: 100%;
    outline: none;
    border: none;
  }
</style>
