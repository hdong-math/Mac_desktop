<template>
  <div class="appstore">
    <iframe id="iframe" src="https://www.apple.com.cn/app-store/"></iframe>
  </div>
</template>

<script>
  export default {
    name: 'Appstore',
    props: {},
    created() {

    },
    methods: {}
  }
</script>

<style scoped>
  .appstore {
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
