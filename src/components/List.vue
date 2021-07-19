<template>
  <div class="list-container">
    <div class="item-container" v-for="item in items" :key="item.name">
      <div class="content">
        <div class="img-container">
          <img
            :src="require(`@/assets/img/menu/${item.img}`)"
            :alt="item.img"
          />
        </div>
        <div class="info">
          <div class="name">{{ item.name }}</div>
          <div class="price">$ {{ item.price }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "List",
  props: ["data"],
  data() {
    return {
      items: [],
    };
  },
  created() {
    this.data.map((item) => {
      if (item.isActive) {
        this.items.push(item);
      }
    });
  },
};
</script>

<style lang="scss" scoped>
.item-container {
  margin: 20px 24px 0px 24px;
  border-radius: 15px;
  -moz-box-shadow: 0 5px 10px rgba(0, 0, 0, 0.5);
  -webkit-box-shadow: 0 5px 10px rgba(0, 0, 0, 0.5);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.5);
  .content {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-around;
    margin: 0 10px 0 10px;
    img {
      width: 120px;
      height: 120px;
      margin-top: 10px;
      margin-bottom: 10px;
      -webkit-filter: drop-shadow(5px 5px 5px rgba(0, 0, 0, 0.2));
      filter: drop-shadow(5px 5px 5px rgba(0, 0, 0, 0.2));
    }
    .info {
      font-family: "SF Pro Bold";
      display: flex;
      flex-direction: column;
      width: 50%;
      align-items: center;
      .name {
        text-align: center;
        color: $dark;
      }
      .price {
        text-align: center;
        color: $light;
        background-color: $secondary;
        padding: 10px;
        border-radius: 25px;
        margin-top: 10px;
      }
    }
  }
}
</style>
