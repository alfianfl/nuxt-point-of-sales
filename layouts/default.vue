<template>
  <div class="wrapper">
    <SideBar />
    <AppHeader />
    <!-- <Alert /> -->
    <div class="">
      <nuxt />
    </div>
  </div>
</template>

<script>
import AppHeader from '@/components/commons/Header'
import SideBar from '@/components/commons/SideBar'

export default {
  components: { AppHeader, SideBar },
  methods: {
    pageStatusHandler(dataPage) {
      this.pageStatus = dataPage
    },
  },
}
</script>

<style>
body {
  margin: 0 !important;
  font-family: 'TT Commons';
}
.wrapper {
  padding-left: 130px;
}
</style>
