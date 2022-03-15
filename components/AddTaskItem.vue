<template>
  <v-dialog v-model="open" max-width="290">
    <template v-slot:activator="{ on }">
      <v-btn icon v-on="on">
        <v-icon>mdi-plus</v-icon>
      </v-btn>
    </template>

    <v-card>
      <v-card-title class="headline teal--text">
        Create New Task
      </v-card-title>

      <v-card-text>
        <v-form ref="form" lazy-validation>
          <v-text-field v-model="form.title" :rules="rules.title" label="Title" required/>
          <v-text-field v-model="form.description" :rules="rules.description" label="Description" required/>
        </v-form>
      </v-card-text>

      <v-card-actions>
        <v-spacer />

        <v-btn color="teal" text @click="save">
          Save
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: "AddTaskItem",

  data() {
    return {
      open: false,
      form: {
        title: null,
        description: null
      },

      rules: {
        title: [
          v => !!v || 'Title is required!',
          v => (!!v && v.length >= 2) || 'Title must be greater than 2 characters'
        ],
        description: [
          v => !!v || 'Description is required!',
          v => (!!v && v.length <= 50) || 'Description must be less than 50 characters'
        ]
      }
    }
  },

  methods: {
    save() {
      if(this.$refs.form.validate()){
        this.$store.dispatch('task/add', this.form)
      }

      this.$refs.form.reset();

      this.open = false;
    }
  },
}
</script>

<style scoped>

</style>
