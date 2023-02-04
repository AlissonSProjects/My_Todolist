<template>
  <div>
    <form @submit.prevent="addTask">
      <input type="text" v-model="newTask" placeholder="Adicionar tarefa">
      <button>Adicionar</button>
    </form>
    <ul>
      <li v-for="task in tasks" :key="task.id" @click="completeTask(task)" :class="{ completed: task.completed, editing: task.editing }">
        <template v-if="task.editing">
          <input type="text" v-model="task.description" @keyup.enter="updateTask(task)">
          <button @click="updateTask(task)">Atualizar</button>
        </template>
        <template v-else>
          {{ task.description }}
          <button @click="removeTask(task)">Remover</button>
          <button @click="editTask(task)">Editar</button>
        </template>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [
        { id: 1, description: 'Fazer compras', completed: false, editing: false },
        { id: 2, description: 'Lavar roupa', completed: false, editing: false },
        { id: 3, description: 'Limpar a casa', completed: false, editing: false },
      ],
    };
  },
  methods: {
    addTask() {
      if (!this.newTask) {
        alert('A tarefa não pode estar em branco');
        return;
      }
      const task = {
        id: this.tasks.length + 1,
        description: this.newTask,
        completed: false,
        editing: false,
      };
      this.tasks.push(task);
      this.newTask = '';
    },
    removeTask(task) {
      this.tasks = this.tasks.filter(t => t.id !== task.id);
    },
    completeTask(task) {
      task.completed = !task.completed;
    },
    editTask(task) {
      task.editing = true;
    },
    updateTask(task) {
      task.editing = false;
    },
  },
};
</script>

<style>
  form {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 1rem;
  }
  form input[type="text"] {
    width: 100%;
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    line-height: 1.5;
    color: #495057;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
  }
  form input[type="text"]:focus {
    color: #495057;
    background-color: #fff;
    border-color: #80bdff;
    outline: 0;
    box-shadow: 0 0 0 0.2rem rgba(0, 123, 255, 0.25);
  }
  form button {
    margin-left: 0.5rem;
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #fff;
    background-color: #007bff;
    border-color: #007bff;
    border-radius: 0.25rem;
    cursor: pointer;
    transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out, border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
  }
  form button:hover {
    color: #fff;
    background-color: #0069d9;
    border-color: #0062cc;
  }
  form button:focus {
    outline: 0;
    box-shadow: 0 0 0 0.2rem rgba(38, 143, 255, 0.5);
  }
  ul {
    list-style: none;
    padding: 0;
  }
  ul li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0.5rem 1rem;
    margin-bottom: 1rem;
    background-color: #fff;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
  }
  ul li.completed {
    background-color: #f8f9fa;
    text-decoration: line-through;
  }
  </style>
  