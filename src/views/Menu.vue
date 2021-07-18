<template>
  <div class="container no-selectable">
    <div class="header">
      <div class="img-container">
        <img src="../assets/img/logo.png" alt="logo" />
      </div>
      <h1>Menú</h1>
    </div>
    <div class="nav-menu" id="nav" :class="{ sticky: active }">
      <div class="scroll-menu">
        <div
          class="item-menu"
          @click="selected = 1"
          :class="{ highlight: selected == 1 }"
        >
          <i class="fa fa-border-all" /> Todo
        </div>
        <div
          class="item-menu"
          @click="selected = 2"
          :class="{ highlight: selected == 2 }"
        >
          <i class="fa fa-hamburger" /> Comidas
        </div>
        <div
          class="item-menu"
          @click="selected = 3"
          :class="{ highlight: selected == 3 }"
        >
          <i class="fa fa-ice-cream" /> Heladería
        </div>
        <div
          class="item-menu"
          @click="selected = 4"
          :class="{ highlight: selected == 4 }"
        >
          <i class="fa fa-wine-bottle" /> Bebidas
        </div>
      </div>
    </div>
    <div class="content">
      <transition name="list">
        <List
          :data="PriceList.comidas"
          v-show="selected == 1 || selected == 2"
        />
      </transition>
      <transition name="list">
        <List
          :data="PriceList.heladeria"
          v-show="selected == 1 || selected == 3"
        />
      </transition>
      <transition name="list">
        <List
          :data="PriceList.bebidas"
          v-show="selected == 1 || selected == 4"
        />
      </transition>
    </div>
  </div>
</template>

<script>
import PriceList from "../static/pricelist.json"; //Data
import List from "../components/List.vue";

export default {
  name: "Menu",
  data() {
    return { PriceList: PriceList, selected: 1, active: false };
  },
  components: { List },
  methods: {
    toggleNavClass() {
      if (this.active == false) {
        return "nav";
      } else {
        return "sticky-nav";
      }
    },
  },
  mounted() {
    window.document.onscroll = () => {
      let navBar = document.getElementById("nav");
      if (window.scrollY > navBar.offsetTop) {
        this.active = true;
      } else {
        this.active = false;
      }
    };
  },
};
</script>

<style lang="scss">
.container {
  display: flex;
  flex-direction: column;
  .header {
    background-color: $primary;
    height: auto;
    text-align: center;
    img {
      padding-top: 10px;
      width: 200px;
      -webkit-filter: drop-shadow(5px 5px 5px rgba(0, 0, 0, 0.2));
      filter: drop-shadow(5px 5px 5px rgba(0, 0, 0, 0.2));
    }
    h1 {
      color: $dark;
      font-family: "SF Pro Heavy";
      font-size: 50px;
      padding-bottom: 10px;
    }
  }
  .img-container {
    position: relative;
  }
  .img-container:after {
    content: " ";
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 99;
  }
  .nav-menu {
    display: flex;
    justify-content: center;
    background-color: $primary;
    padding-top: 10px;
    padding-bottom: 10px;
    .scroll-menu {
      display: flex;
      overflow-y: auto;
      .item-menu {
        background-color: $light;
        font-family: "SF Pro Light";
        text-align: center;
        color: $dark;
        border-radius: 25px;
        margin-left: 10px;
        padding: 10px;
        cursor: pointer;
        display: flex;
        align-items: center;
        -webkit-tap-highlight-color: transparent;
        i {
          margin-right: 4px;
        }
      }
      .highlight {
        background-color: $secondary;
        color: $light;
      }
    }
  }
  .content {
    margin: 0 0 20px 0;
    align-self: center;
    max-width: 800px;
  }
}

.sticky {
  position: fixed;
  width: 100%;
  z-index: 99;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  -moz-box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  -webkit-box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
}

.no-selectable {
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -o-user-select: none;
  user-select: none;
}

.list-enter {
  visibility: hidden;
  height: 0;
  margin: 0;
  padding: 0;
  opacity: 0;
}

.list-enter-active {
  transition: opacity 0.3s 0.1s, height 0.3s;
}
</style>
