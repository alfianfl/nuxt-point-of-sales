<template>
  <aside class="side-bar bg-black">
    <div class="logo box-size bg-dark-grey">
      <span class="title">POS</span>
    </div>
    <nav>
      <ul class="list-nostyle">
        <li v-for="(nav, i) in menu" :key="i">
          <nuxt-link :to="nav.url" class="box-size">
            <span class="icon" :class="'icon-' + nav.icon"></span>
            <span class="text-white">{{ nav.title }}</span>
          </nuxt-link>
        </li>
      </ul>
    </nav>
  </aside>
</template>

<script>
export default {
  name: 'SideBar',
  data() {
    return {
      menu: [
        {
          icon: 'home-page',
          title: 'Home page',
          url: '/',
          active: true,
        },
        {
          icon: 'point-of-sale',
          title: 'Point of Sale',
          url: '/point-of-sale',
          active: false,
        },
        {
          icon: 'inventory',
          title: 'Inventory',
          url: '/inventory',
          active: false,
        },
      ],
    }
  },
  methods: {},
}
</script>

<style lang="css" scoped>
::-webkit-scrollbar {
  width: 5px;
}

::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px grey;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb {
  background: rgba($color: #fff, $alpha: 0.4);
}

::-webkit-scrollbar-thumb:hover {
  background: #b30000;
}
.side-bar {
  position: fixed;
  top: 0;
  left: 0;
  width: 130px;
  height: 100vh;
  overflow-y: auto;
}

li {
  border-top: 1px solid #c4c4c4;
  border-bottom: 1px solid #c4c4c4;
}
a {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
ul {
  margin-top: 8em;
}

.nuxt-link-exact-active {
  background-color: #fd4513;
}

.box-size {
  padding: 26px 0;
}

.logo {
  position: fixed;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: inherit;
}
.title {
  color: #fd4513;
  font-family: 'Druk Text';
  font-weight: 600;
}
</style>
