<template>
  <div class="todo-item">
    <div class="todo__date">{{ todo.dates }}</div>

    <div class="todo__content">
      <input
        type="text"
        class="description"
        :disabled="!editState"
        :value="todo.text"
        @input="$emit('input', $event)"
      />

      <div class="btn-block">
        <button class="btn complete" @click="editState = true"><img src="../assets/img/pencil.png"></button>

        <button class="btn delete" @click="$emit('remove-todo')"><img src="../assets/img/close.png"></button>

        <button class="btn check" @click="editState = false"><img src="../assets/img/check.png"></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  data() {
    return { editState: false };
  },
  methods: {
    onEndEdit() {
      this.editState = false;
      this.$emit("end-edit");
    },
  },
};
</script>


<style lang="scss">
.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 46px;
  margin: 17px 25px;
  background: #ffffff;
}
.todo__date {
  height: 46px;
  font-size: 14px;
  line-height: 46px;
  font-family: "Roboto";
  background: #ffffff;
  border-bottom: 1px solid #868686;
}
.todo__content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 490px;
  height: 46px;
  border-bottom: 1px solid #868686;
}

.description {
   width:80%;
  font-family: "Roboto";
  font-size: 16px;
  line-height: 20px;
  color: rgba(0, 0, 0, 0.82);
  cursor: pointer;
  height: 20px;
  overflow: auto;
}
.btn-block {
  display: flex;
  margin-left: 7px;
}
.btn {
  background: #62abd9;
  border-radius: 5px;
  margin-bottom: 9px;
  width: 36px;
  height: 36px;
}
.complete {
  margin-right: 15px;
}

img {
  width: 20px;
  height: 20px;
}
/*576px - 768px*/
@media screen and (max-width: 768px) {
   .todo-item {
   margin: 17px 20px;
}
   .todo__content {
   width: 370px;
}
.description{
   width:290px;
}
   .btn {
   width: 30px;
   height: 30px;
}
}
@media screen and (max-width: 576px) {
   .todo-item {
   margin: 17px 10px;
}
   .todo__date {
   width:20%;
  font-size: 12px;
  line-height:25px;
}
   .todo__content {
   width: 75%;
}
   .description{
   width: 80%;
   font-size: 14px;
}
.btn-block {
  display: table-column;
  margin-bottom: 5px;
}
   .btn {
   width: 25px;
   height: 25px;

}
.complete {
  margin-right: 0px;
  margin-bottom: 5px;
}
}
@media screen and (max-width: 576px) {
   .todo__date {
  font-size: 10px;
}
}

/*0px - 576px*/
</style>