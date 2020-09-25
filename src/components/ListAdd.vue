<template>
  <form :class="classList" @submit.prevent="addList">
    <input
      v-model="title"
      type="text"
      class="text-input"
      placeholder="Add new list"
      @focusin="startEditing"
      @focusout="finishEditing"
    />
    <button type="submit" class="add-button" v-if="isEditing || titleExists">
      Add
    </button>
  </form>
</template>
<script>
export default {
  data() {
    return {
      title: "",
      isEditing: false, //フォーカス初期値
    };
  },

  //監視
  computed: {
    //------------------------
    classList() {
      const classList = ["addlist"];
      if (this.isEditing) {
        classList.push("active");
      }
      if (this.titleExists) {
        classList.push("addable");
      }
      return classList;
    },
    //------0文字以上入力していたら表示---------
    titleExists() {
      return this.title.length > 0;
    },
  },

  //-------メソッド-----------
  methods: {
    addList() {
      this.$store.dispatch("addlist", { title: this.title });
      this.title = "";
    },
    startEditing() {
      this.isEditing = true;
    },
    finishEditing() {
      this.isEditing = false;
    },
  },
};
</script>
