<template>
  <q-page class="bg-green-3 column">
<div class="row q-pa-sm bg primary">
  Add new task!!!
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
