<template>
  <div class="list-container">
    <div class="item-container" v-for="(item, index) in data" :key="index.id">
      <div class="content" v-if="item.isActive">
        <div class="photo img-container">
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
};
</script>

<style lang="scss" scoped>
.list-container {
  .item-container {
    align-self: center;
    margin: 20px 24px 0px 24px;
    border-radius: 15px;
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.5);
    -moz-box-shadow: 0 5px 10px rgba(0, 0, 0, 0.5);
    -webkit-box-shadow: 0 5px 10px rgba(0, 0, 0, 0.5);
    .content {
      display: flex;
      flex-direction: row;
      padding: 20px;
      justify-content: space-around;
      align-items: center;
      .photo {
        img {
          -webkit-filter: drop-shadow(2px 2px 2px rgba(0, 0, 0, 0.2));
          filter: drop-shadow(2px 2px 2px rgba(0, 0, 0, 0.2));
          width: 100px;
        }
      }
      .info {
        margin: 5px;
        text-align: center;
        display: flex;
        flex-direction: column;
        align-items: center;
        .name {
          font-family: "SF Pro Bold";
          color: $dark;
          margin-bottom: 10px;
        }
        .price {
          font-family: "SF Pro Bold";
          color: $light;
          background-color: $secondary;
          border-radius: 25px;
          padding: 5px;
          width: 150px;
        }
      }
    }
  }
}
</style>
