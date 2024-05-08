<template>
  <div id="todo">
    <div class="container mt-5">
      <div class="row justify-content-md-center">
        <div class="col-md-8 bg-white p-3">
          <h1 class="text-center">Bienvenue!</h1>
          <p class="text-center"> Créez votre <span class="badge bg-primary">liste personnalisée</span> de choses à
            faire</p>
          <hr>

          <!-- Button Ajouter-->
          <div class="d-flex align-items-center py-2">
            <input v-model="newItemText" class="borders form-control flex-grow-1">
            <button class="btn btn-primary ms-2" v-on:click="addNewToDO">Ajouter</button>
          </div>

          <div class="d-flex justify-content-end py-2">
            <label class="form-check ms-2 small">Afficher / Masquer les tâches terminées</label>
            <input type="checkbox" v-model="hide" class="borders form-check-input ms-2">
          </div>

          <hr>
          <div class="d-flex align-items-center justify-content-between  py-1" v-for="t in hiddentasks" :key="t.task">
            <div>{{ t.task }}</div>
            <div>
              <input type="checkbox" v-model="t.completed" class="borders form-check-input" />
              <button class="btn btn-outline-primary ms-2 btn-sm" v-on:click="deleteToDO">Effacer</button>
            </div>

          </div>

        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: 'App',
  /**
   * @property {AppData} data - The data object of the component.
   */
  data() {
    return {
      name: 'Aleks',
      tasks: [],
      hide: true,
      newItemText: ''
    };
  },
  computed: {
    /**
     * @property {Task[]} hiddentasks - The filtered list of tasks based on the hide property.
     */
    hiddentasks() {
      return this.hide ? this.tasks.filter(t => !t.completed) : this.tasks;
    }
  },
  methods: {
    /**
     * Adds a new task to the tasks list.
     */
    addNewToDO() {
      if (this.newItemText.trim()) {
        this.tasks.push({ task: this.newItemText, completed: false });
        this.updateLocalStorage();
        this.newItemText = '';
      }
    },
    /**
     * Deletes a task from the tasks list.
     * @param {number} index - The index of the task to be deleted.
     */
    deleteToDO(index) {
      this.tasks.splice(index, 1);
      this.updateLocalStorage();
    },
    /**
     * Updates the local storage with the current tasks list.
     */
    updateLocalStorage() {
      localStorage.setItem('tasksList', JSON.stringify(this.tasks));
    }
  },
  watch: {
    /**
     * Watches for changes in the tasks list and updates the local storage.
     */
    tasks: {
      handler() {
        this.updateLocalStorage();
      },
      deep: true // Watches for deep modifications
    }
  },
  created() {
    /**
     * Retrieves the tasks list from the local storage on component creation.
     */
    let data = localStorage.getItem('tasksList');
    if (data) {
      this.tasks = JSON.parse(data);
    }
  }
};

</script>

<style>
html body {
  background-color: rgb(12, 85, 231);

  margin: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

h1 {
  color: rgb(12, 85, 231) !important;
}

.borders {
  border: 0.2px solid rgb(12, 85, 231) !important;
  border-radius: 5px !important;
}

delete-button {
  color: white;
  background-color: red;
  border: none;
  border-radius: 5px;
  
}
</style>
