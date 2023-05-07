<template>
  <q-page class="bg-purple-3 column">
    <div class="row q-pa-sm bg-pink-2">
      <q-input
        @keyup.enter="addTask"
        filled
        v-model="newTask"
        dense
        square
        bg-color="white"
        class="col"
        placeholder="  Add task"
      />
      <q-btn round dense flat icon="send" @click="addTask" />
    </div>

    <q-list separator bordered>
      <q-item
        @click="task.done = !task.done"
        clickable
        :class="{ 'done bg-pink-2': task.done }"
        v-for="(task, index) in tasks"
        :key="task.title"
        v-ripple
      >
        <q-item-section avatar top>
          <q-checkbox v-model="task.done" val="cyan" color="black" />
        </q-item-section>
        <q-item-section>
          <q-item-label
            ><b>{{ task.title }}</b></q-item-label
          >
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn
            @click.stop="deleteTask(index)"
            dence
            outline
            style="color: black"
            label="Delete"
          />
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: [
        {
          title: "hello",
          done: false,
        },
      ],
    };
  },
  methods: {
    deleteTask(index) {
      this.$q
        .dialog({
          title: "Confirm",
          message: "Would you like to delete the task?",
          cancel: true,
          persistent: true,
        })
        .onOk(() => {
          this.tasks.splice(index, 1);
          this.$q.notify("Task deleted!");
        });
    },
    addTask() {
      this.tasks.push({
        title: this.newTask,
        done: false,
      });
      this.newTask = "";
    },
  },
};
</script>


<style lang='scss'>
.done {
  .q-item__label {
    text-decoration: line-through;
    color: grey;
  }
}
</style>