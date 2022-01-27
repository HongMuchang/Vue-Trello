<template>
  <div>
    <header>
      <!-- Trello -->
      <div class="header_images">
        <img src='../assets/icon.png' class="icon">
      </div>
    </header>
    <main>
      <div class="main_top">
        <p class="info-line alltask">All : {{ totalCardCount }} 件</p>
      </div>
        <ListAdd />
      <div class="list-index">
        <draggable :list="lists" @end="movingList" class="list-index">
          <List
            v-for="(item, index) in lists"
            :key="item.id"
            :title="item.title"
            :cards="item.cards"
            :listIndex="index"
            @change="movingCard"
          />
        </draggable>
      </div>
    </main>
  </div>
</template>
<script>
import draggable from "vuedraggable";
import ListAdd from "./ListAdd.vue";
import List from "./List";
import { mapState } from "vuex";
export default {
  components: {
    ListAdd,
    List,
    draggable,
  },
  computed: {
    ...mapState(["lists"]),
    totalCardCount() {
      return this.$store.getters.totalCardCount;
    },
  },
  methods: {
    movingCard: function() {
      this.$store.dispatch("updateList", { lists: this.lists });
    },
    movingList: function() {
      this.$store.dispatch("updateList", { lists: this.lists });
    },
  },
};
</script>
