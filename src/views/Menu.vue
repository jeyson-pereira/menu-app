<template>
  <div class="container no-selectable">
    <div class="header">
      <div class="img-container">
        <img src="../assets/img/logo.png" alt="logo" />
      </div>
      <h1>Menú</h1>
    </div>
    <div class="nav-menu" :class="{ sticky: active }">
      <div class="scroll-menu" :class="{ center: desktop }" id="nav">
        <div
          class="item-menu"
          @click="selected = 1"
          :class="{ highlight: selected == 1 }"
        >
          <i class="fa fa-border-all" />
          <h3>Todo</h3>
        </div>
        <div
          class="item-menu"
          @click="selected = 2"
          :class="{ highlight: selected == 2 }"
        >
          <i class="fa fa-hamburger" />
          <h3>Comidas</h3>
        </div>
        <div
          class="item-menu"
          @click="selected = 3"
          :class="{ highlight: selected == 3 }"
        >
          <i class="fa fa-ice-cream" />
          <h3>Heladería</h3>
        </div>
        <div
          class="item-menu"
          @click="selected = 4"
          :class="{ highlight: selected == 4 }"
        >
          <i class="fa fa-wine-bottle" />
          <h3>Bebidas</h3>
        </div>
      </div>
    </div>
    <div class="body-content" :class="{ 'unmount-nav': active }">
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
    return {
      PriceList: PriceList,
      selected: 1,
      active: false,
      desktop: undefined,
      windowWidth: window.innerWidth,
    };
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
    onResize() {
      this.windowWidth = window.innerWidth;
      if (this.windowWidth > 400) {
        this.desktop = true;
      } else {
        this.desktop = false;
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
  created() {
    this.onResize();
    window.addEventListener("resize", this.onResize);
  },
  destroyed() {
    window.removeEventListener("resize", this.onResize);
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
    display: flex;
    flex-direction: column;
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
    background-color: $primary;
    padding-top: 10px;
    padding-bottom: 10px;
    overflow: auto;
    .scroll-menu {
      margin: 0 5px 0 5px;
      display: flex;
      .item-menu {
        background-color: $light;
        color: $dark;
        border-radius: 25px;
        padding: 10px;
        cursor: pointer;
        display: flex;
        align-items: center;
        margin: 0 5px 0 5px;
        -webkit-tap-highlight-color: transparent;
        box-shadow: 0 2px 2px rgba(0, 0, 0, 0.2);
        -moz-box-shadow: 0 2px 2px rgba(0, 0, 0, 0.2);
        -webkit-box-shadow: 0 2px 2px rgba(0, 0, 0, 0.2);
        h3 {
          margin-left: 5px;
          font-family: "SF Pro Light";
          font-weight: normal;
          font-size: 16px;
        }
        i {
          .fa {
            line-height: 0%;
          }
        }
      }
      .item-menu:active {
        background-color: $secondary;
        color: $light;
      }
      .highlight {
        background-color: $secondary;
        color: $light;
      }
    }
    .center {
      justify-content: center;
    }
  }
  .body-content {
    margin-bottom: 20px;
    display: flex;
    flex-direction: column;
    align-self: center;
    min-width: 230px;
    max-width: 600px;
  }
  .unmount-nav {
    margin-top: 60px;
  }
}

.sticky {
  min-width: 100%;
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 100;
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
