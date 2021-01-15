<template>
  <header>
    <h1 class="mainTitle">To-DO list</h1>
  </header>
  <div class="section">
    <div class="container">
      <div class="row center-xs">
        <div class="col-xs-3">
          <input
            class="input"
            type="text"
            v-model.lazy="inputValue"
            placeholder="Add new item"
          />
        </div>
        <div class="col-xs-3">
          <Button
            @click="addItem()"
            class="button"
            label="AddItem" />
          <input
            @change="filteredItems()"
            type="checkbox"
            id="UncompletedTasks"
            name="UncompletedTasks"
            class="checkbox">
          <label
            for="UncompletedTasks"
            class="checkLabel">
          Uncompleted
          </label>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="row">
        <div :key="index" v-for="({ toDo, completed }, index) in allItemsList">
          <div class="col-xs-12">
            <div v-if="toDo" class="listItemWrapper">
              <h2
                :class="{ toDotextChecked: completed }"
                style="margin-left: 10px"
              >
                {{ toDo }}
              </h2>
              <Button
                @click="deleteItem(index)"
                class="button"
                label="Delete"
              />
              <input
                type="checkbox"
                @change="isCompleted(index)"
                class="checkbox"
                :checked="completed"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import 'flexboxgrid';

import { defineComponent } from 'vue';

import Button from './components/button/button.vue';

type Item = {
  toDo: string;
  completed: boolean;
}

type Data = {
  done: boolean;
  unDone: boolean;
  inputValue: string;
  allItemsList: Item [];
};

const ToDoList = defineComponent({
  components: {
    Button,
  },

  data(): Data {
    return {
      done: false,
      unDone: false,
      inputValue: '',
      allItemsList: [
        {
          toDo: '',
          completed: false,
        },
      ],
    };
  },

  methods: {
    addItem() {
      if (this.inputValue) {
        this.allItemsList.push({
          toDo: this.inputValue,
          completed: false,
        });
        this.inputValue = '';
      }
    },

    isCompleted(index: number) {
      this.allItemsList[index].completed = !this.allItemsList[index].completed;
    },

    deleteItem(index: number) {
      return this.allItemsList.splice(index, 1);
    },

    filteredItems() {
      this.allItemsList.filter((item, index) => {
        if (!this.allItemsList[index].completed) {
          console.log(item);
          return item;
        } if (this.allItemsList[index].completed) {
          console.log(item.completed);
          return item.completed;
        } return item;
      });
    },
  },

  computed: {
    allToDosFilter(): Item[] {
      return this.allItemsList.filter((item) => {
        if (this.done) {
          return item.completed;
        } if (this.unDone) {
          return !item.completed;
        } return item;
      });
    },
  },
});

export default ToDoList;
</script>
<style src="./app.scss" lang="scss" scoped></style>
