<template>
  <v-app>
    <v-main>
      <v-container class="my-5">
        <v-card class="pa-5 card-background">
          <v-card-title class="title"><b>CREATE YOUR TO-DO</b></v-card-title>

          <!-- Input for new task with Add button beside it -->
          <v-row class="input-row mb-4">
            <v-col cols="12" md="10">
              <v-text-field
                v-model="newTask"
                label="ADD TASK"
                outlined
                dense
                class="input-background"
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="2">
              <v-btn color="primary" @click="addTask" block>Add</v-btn>
            </v-col>
          </v-row>

          <!-- List of tasks -->
          <v-list class="tasks-list">
            <v-row v-for="(task, index) in tasks" :key="index" no-gutters>
              <v-col cols="12">
                <v-card outlined class="custom-card d-flex align-center justify-space-between mt-4">
                  <!-- Checkbox on the left -->
                  <v-card-actions class="checkbox-container">
                    <v-checkbox v-model="task.completed" class="me-3"></v-checkbox>
                  </v-card-actions>

                  <!-- Task title in the middle -->
                  <v-card-title class="flex-grow-1">
                    <span :class="{ 'done-task': task.completed }">{{ task.title }}</span>
                  </v-card-title>

                  <!-- Edit and Delete buttons on the right -->
                  <v-card-actions>
                    <v-btn text class="border bg-warning me-2" color="white" @click="editTask(index)">
                      Edit
                    </v-btn>
                    <v-btn text class="border bg-red" color="white" @click="deleteTask(index)">
                      Delete
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-col>
            </v-row>
          </v-list>
        </v-card>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: [
        { title: "Design a website", completed: false },
        { title: "Develop the website", completed: false },
        { title: "Publish the website", completed: false },
      ],
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({ title: this.newTask, completed: false });
        this.newTask = "";
      }
    },
    editTask(index) {
      const task = prompt("Edit task:", this.tasks[index].title);
      if (task) {
        this.tasks[index].title = task;
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>

<style scoped>
.card-background {
  background: linear-gradient(to bottom, #e0f7fa, #80deea); /* Gradient from light cyan to cyan */
}

.title {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 20px;
}

.done-task {
  text-decoration: line-through;
  color: gray;
}

.input-row {
  background-color: #f5f5f5; /* Light gray background for the input area */
  padding: 10px;
  border-radius: 4px;
}

.input-background .v-text-field {
  background-color: #ffffff; /* White background for the text field */
}

.tasks-list {
  background: linear-gradient(to bottom, #b3e5fc, #81d4fa); /* Gradient from light blue to deeper blue */
  border-radius: 4px;
  padding: 10px;
}

.custom-card {
  background-color: #ffffff;
  border: 1px solid #0c0808;
  border-radius: 4px;
  padding: 10px;
}

.border {
  border-radius: 4px;
}

.bg-warning {
  background-color: #ffca28 !important; /* Bright yellow */
}

.bg-red {
  background-color: #f44336 !important; /* Red color */
}

.me-3 {
  margin-right: 12px;
}

.me-2 {
  margin-right: 8px;
}

/* Align checkbox properly */
.checkbox-container {
  display: flex;
  align-items: center; /* Align checkbox vertically */
}

/* Responsive adjustments */
@media (max-width: 600px) {
  .title {
    font-size: 1.2rem; /* Smaller font for smaller screens */
  }

  .input-row {
    flex-direction: column; /* Stack input and button vertically on small screens */
  }

  .input-background .v-text-field {
    margin-bottom: 10px; /* Add margin to separate input and button */
  }

  .custom-card {
    flex-direction: column; /* Stack items vertically on small screens */
    padding: 20px;
  }

  .v-btn {
    width: 0%; /* Make buttons full-width on mobile */
    margin-bottom: 8px;
  }

  .tasks-list {
    padding: 8px; /* Adjust padding for smaller screens */
  }
}

@media (min-width: 601px) and (max-width: 960px) {
  .title {
    font-size: 1.3rem; /* Medium font size for medium screens */
  }

  .input-row {
    flex-direction: row; /* Align input and button horizontally on medium screens */
  }

  .input-background .v-text-field {
    margin-right: 10px; /* Space between input and button */
  }

  .v-btn {
    margin-bottom: 0; /* Remove margin for buttons when aligned horizontally */
  }
}

@media (min-width: 961px) {
  .title {
    font-size: 1.5rem; /* Larger font size for larger screens */
  }

  .input-row {
    flex-direction: row; /* Align input and button horizontally on larger screens */
  }
}
</style>
