<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
        @keyup.enter="addTask"
        v-model="newTask"
        class="col"
        bg-color="white"
        filled
        square
        placeholder="Добавить задание"
        dense
      >
        <template v-slot:append>
          <q-btn round dense flat icon="add" @click="addTask" />
        </template>
      </q-input>
    </div>
    <q-list class="bg-white" bordered separator>
      <q-item
        v-ripple
        v-for="(task, index) in tasks"
        :key="task.title"
        @click="taskDone(index)"
        clickable
        :class="{ 'done bg-blue-1': task.done }"
      >
        <q-item-section avatar>
          <q-checkbox v-model="task.done" color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done">
          <q-btn
            @click.stop="deleteTask(index)"
            flat
            dense
            round
            color="primary"
            icon="delete"
          />
        </q-item-section>
      </q-item>
    </q-list>
    <div v-if="!tasks.length" class="no-tasks absolute-center">
      <q-icon name="check" size="100px" color="primary" />
      <div class="text-h5 text-primary text-center">Нет заданий</div>
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },
  methods: {
    taskDone(index) {
      this.tasks[index].done = !this.tasks[index].done;
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    deleteTask(index) {
      this.$q
        .dialog({
          title: "Confirm",
          message: "Удалить задание?",
          cancel: true,
          persistent: true,
        })
        .onOk(() => {
          this.tasks.splice(index, 1);
          localStorage.setItem("tasks", JSON.stringify(this.tasks));
          this.$q.notify("Задание удалено!");
        });
    },
    addTask() {
      this.newTask !== "" &&
        this.tasks.push({
          title: this.newTask,
          done: false,
        });
      this.newTask = "";
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
  },
  created() {
    this.tasks = JSON.parse(localStorage.getItem("tasks"));
  },
};
</script>

<style lang="scss">
.done {
  .q-item__label {
    text-decoration: line-through;
    color: #bbb;
  }
}
.no-tasks {
  display: flex;
  flex-direction: column;
  align-items: center;
  opacity: 0.5;
}
</style>
