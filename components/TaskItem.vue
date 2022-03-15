<template>
  <v-list-item v-if="task" inactive>
    <v-list-item-action>
      <v-btn icon :color="iconColor" @click="changeStatus">
        <v-icon v-text="icon"/>
      </v-btn>
    </v-list-item-action>

    <v-list-item-content>
      <v-list-item-title v-text="task.title" />

      <v-list-item-subtitle v-text="task.description" />
    </v-list-item-content>

    <v-list-item-action>
      <v-btn icon color="error" @click="deleteTask">
        <v-icon>mdi-trash-can-outline</v-icon>
      </v-btn>
    </v-list-item-action>
  </v-list-item>
</template>

<script>
export default {
  name: "TaskItem",

  props: {
    task: {
      type: Object,
      default: null
    },
  },

  computed: {
    icon() {
      return this.task.done ? 'mdi-check' : 'mdi-reload-alert';
    },

    iconColor(){
      return this.task.done ? 'success' : 'warning';
    }
  },

  methods: {
    changeStatus() {
      this.$store.dispatch('task/done', {
        id: this.task.id, done: !this.task.done
      });
    },

    deleteTask(){
      this.$store.dispatch('task/remove', this.task.id)
    }
  },
}
</script>

<style scoped>

</style>
