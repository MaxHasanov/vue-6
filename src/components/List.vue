<template>
  <div class="list">
    <ul class="list_title">
      <li>Date</li>
      <li>Category</li>
      <li>Count</li>
    </ul>
    <div v-for="item of list" :key="item.id" class="list_item">
      <div> {{ item.data }} </div>
      <div> {{ item.category }} </div>
      <div> {{ item.count }}$ </div>
      <span class="dot" @click="callContextMenu($event, item)">&#10247;</span>
      <ContextMenu></ContextMenu>
    </div>
  </div>
</template>

<script>
import ContextMenu from './ContextMenu.vue';
export default {
  name: 'List',
  components: {
    ContextMenu,
  },
  mounted() {
    this.$context.EventEmitter.$on("show", this.show);
  },
  computed: {
    list() {
      return this.$store.getters.getPaymentsList
    }
  },
  methods: {
    callContextMenu(event, item) {
      this.$context.show(event.currentTarget, item);
    }
  },
};
</script>

<style lang="scss">
.list {
  width: 780px;
  margin: 0 auto;
  border-radius: 10px;
  background-color: #ddd;
  padding: 4px 0;
  box-sizing: border-box;

  &_title {
    list-style-type: none;
    display: flex;
    justify-content: space-evenly;
    font-weight: bold;
  }


  &_item {
    display: flex;
    justify-content: space-between;
    padding: 10px 25px;
  }
}

.context-menu {
  cursor: pointer;
  text-decoration: none;
}

.dot {
  cursor: pointer;
}
</style>