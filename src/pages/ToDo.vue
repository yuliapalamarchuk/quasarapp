<template>
  <q-page class="bg-purple-3 column">
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
      tasks: [
        {
          title: "hello",
          done: false,
        },
        {
          title: "hello2",
          done: false,
        },
        {
          title: "hello3",
          done: false,
        },
      ],
    };
  },
  methods: {
    deleteTask(index) {
      this.tasks.splice(index, 1);
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