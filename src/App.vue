<template>
  <div id="app">
    <div class="container mt-4">
      <div class="row">
        <div class="col-lg-2"></div>
        <div class="col-lg-8 col-md-12 col-sm-12 col-xs-12">
          <div class="card shadow">
            <card-header title="My Tasks"></card-header>
            <div class="card-body">
              <skin
                :change-skin-black="changeSkinBlack"
                :change-skin-blue="changeSkinBlue"
                :change-skin-green="changeSkinGreen"
              ></skin>
              <to-do-form @add-todo="addToDo"></to-do-form>
              <div class="custom-control custom-checkbox">
                <ol>
                  <li v-for="todo in todos" :key="todo.id">
                    <to-do-item
                      :label="todo.label"
                      :done="todo.done"
                      :id="todo.id"
                      :decoration="todo.decoration"
                      @checkbox-changed="updateDoneStatus(todo.id)"
                      @task-edited="editToDo(todo.id, $event)"
                      @task-deleted="deleteToDo(todo.id)"
                    ></to-do-item>
                  </li>
                  <br />
                  <input
                    type="text"
                    disabled
                    name
                    id
                    class="form-control text-center"
                    :value="completedTasks"
                  />
                </ol>
              </div>
            </div>
          </div>
        </div>
        <div class="col-lg-2"></div>
      </div>
    </div>
  </div>
</template>

<script>
import ToDoItem from "./components/ToDoItem";
import CardHeader from "./components/Card/CardHeader";
import ToDoForm from "./components/ToDoForm";
import uniqueId from "lodash.uniqueid";

export default {
  name: "app",
  components: {
    ToDoItem,
    ToDoForm,
    CardHeader
  },
  data() {
    return {
      todos: [
        {
          id: uniqueId("todo-"),
          label: "Learn Vue",
          done: false,
          decoration: "none"
        },
        {
          id: uniqueId("todo-"),
          label: "Create a Vue project with the CLI",
          done: false,
          decoration: "none"
        },
        {
          id: uniqueId("todo-"),
          label: "Machine Learning Python",
          done: false,
          decoration: "none"
        },
        {
          id: uniqueId("todo-"),
          label: "Live your best",
          done: false,
          decoration: "none"
        },
        {
          id: uniqueId("todo-"),
          label: "Create a to-do list app",
          done: false,
          decoration: "none"
        },
        {
          id: uniqueId("todo-"),
          label: "Read the 4-Hour Workweek book",
          done: false,
          decoration: "none"
        }
      ]
    };
  },
  methods: {
    addToDo(newTodo) {
      this.todos.push({
        id: uniqueId("todo-"),
        label: newTodo,
        done: false
      });
    },
    updateDoneStatus(toDoId) {
      const toDoToUpdate = this.todos.find(task => task.id === toDoId);
      toDoToUpdate.done = !toDoToUpdate.done;

      if (toDoToUpdate.done) {
        toDoToUpdate.decoration = "line-through";
      } else {
        toDoToUpdate.decoration = "none";
      }
    },
    deleteToDo(toDoId) {
      const taskIndex = this.todos.findIndex(task => task.id === toDoId);
      this.todos.splice(taskIndex, 1);
      this.$nextTick(() => {
        this.$refs.taskTitle.focus();
      });
    },
    editToDo(toDoId, newLabel) {
      const toDoToEdit = this.todos.find(task => task.id === toDoId);
      toDoToEdit.label = newLabel;
    }
  },
  computed: {
    completedTasks() {
      const numberFinishedItems = this.todos.filter(item => item.done).length;

      if (numberFinishedItems < 1) {
        return `You haven't not completed any task yet `;
      }
      if (numberFinishedItems === this.todos.length) {
        return `Bodacious! Sit back and relax`;
      }

      if (this.todos.length - numberFinishedItems === 1) {
        return `Superb! One task to go`;
      }

      return `${numberFinishedItems} out of ${this.todos.length} tasks completed`;
    }
  }
};
</script> 