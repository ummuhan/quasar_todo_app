<template>
  <q-page class="bg-green-3 column">
    <div class="row q-pa-sm bg primary">
      <q-input
        class="col"
        square
        bg-color="white"
        filled
        bottom-slots
        v-model="newTask"
        @keyup.enter="addTask"
        label="New Task"
        dense
      >
        <template v-slot:before>
          <q-icon name="event" color="white" />
        </template>
        <template v-slot:append>
          <q-btn @click="addTask" round dense flat icon="add" />
        </template>
      </q-input>
    </div>

    <q-list class="bg-white" separator bordered>
      <q-item
        v-for="(task, index) in tasks"
        :key="task.title"
        @click="task.done = !task.done"
        :class="{ 'done bg-green-1': task.done }"
        clickable
        v-ripple
      >
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            class="no-pointer-events"
            color="primary"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn
            @click.stop="deleteTask(index)"
            round
            dense
            color="secondary"
            icon="delete"
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
          title: "get egg",
          done: false,
        },
        {
          title: "get milk",
          done: false,
        },
        {
          title: "get nuts",
          done: false,
        },
      ],
    };
  },
  methods: {
    deleteTask(index) {
      this.tasks.splice(index, 1);
      this.$q.notify({
        message: "Deleted....",
        color: "Green",
      });
    },
    addTask() {
      this.tasks.push({
        title:this.newTask,
        done:false
      })
      this.$q.notify({
        message: "Successfully added....",
        color: "Green",
      });
    },
  },
};
</script>

<style lang="scss">
.done {
  .q-item__label {
    text-decoration: line-through;
    color: rgb(42, 88, 73);
  }
}
</style>
