<template>
  <header class="main-header">
    <nav>
      <!-- <div class="flex iems-center">
                <span
                    v-if="$route.name === 'index'"
                    class="mr-8 icon icon-home-page"
                ></span>
                <span
                    v-else-if="$route.name === 'day-begin-end'"
                    class="mr-8 icon icon-history"
                ></span>
                <span
                    v-else
                    class="mr-8 icon"
                    :class="'icon-' + $route.name"
                ></span>
                <span class="title">{{
                    $route.name === 'index' ? 'Homepage' : $route.name
                }}</span>
            </div> -->

      <div>
        <div class="nav-item flex">
          <span class="mr-8 icon-location"></span><label>test</label>
        </div>
        <div class="nav-item flex">
          <span class="mr-8 icon-credit-card"></span><label>test</label>
        </div>
        <div class="nav-item flex">
          <span class="mr-8 icon-user"></span><label>test</label>
        </div>
        <div class="nav-item flex">
          <span class="mr-8 icon-history"></span><label>test</label>
        </div>
        <div class="util-button space-x-4">
          <nuxt-link class="icon-setting" to="/settings"></nuxt-link>
          <span class="dropdown-notification">
            <button class="icon-bell-o"></button>
          </span>
          <button class="icon-logout"></button>
        </div>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'HeaderPage',
  props: {
    title: {
      type: String,
      required: true,
    },
    icon: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      isOpenModal: false,
      activeModal: '',
      isCustomerWalkInCountButton: false,
      isNotificationButton: false,
      notificationData: [],
      userData: {},
      locationName: {},
      time: '',
      poleTextIdle: '',
      startIndex: 0,
      endIndex: 20,
      textLength: null,
      timerId: null,
      timer: 0,
      count: 0,
      // loginData: {}
    }
  },
  watch: {
    timer(newTime) {
      if (newTime === -1) {
        this.count += 1
        this.showPole()
      }
    },
  },
  methods: {},
}
</script>

<style scoped>
.title {
  font-family: 'Druk Text';
  font-size: 26px;
  line-height: 30px;
  font-weight: 600;
  text-transform: uppercase;
  margin-top: 4px;
}
.dropdown-notification {
  position: relative;
  top: 0;
  left: 0;
}
.icon {
  font-size: 3em;
  color: #394049;
}

.util-button {
  cursor: pointer;
  background-color: #fff;
  font-size: 1.5em;
  border: none;
  color: #000;
}

.nav-item {
  padding: 0.6em;
  display: flex;
  background-color: #f6f6f6;
}
label {
  font-family: 'TT Commons';
  margin-top: 4px;
  line-height: 20px;
  place-self: self-end;
}
.main-header {
  display: flex;
  padding: 24px 0;
  background-color: #fff;
  color: #394049;
  border-bottom: 1px solid #394049;
}

nav {
  width: 100%;
  display: flex;
  justify-content: space-between;
}

nav div {
  margin: 0 12px;
  display: flex;
  align-items: center;
}
</style>
