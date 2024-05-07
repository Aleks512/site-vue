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
  data() {
    return {
      name: 'Aleks',
      tasks: [],
      hide: true,
      newItemText: ''
    };
  },
  computed: {
    hiddentasks() {
      return this.hide ? this.tasks.filter(t => !t.completed) : this.tasks;
    }
  },
  methods: {
    addNewToDO() {
      if (this.newItemText.trim()) {
        this.tasks.push({ task: this.newItemText, completed: false });
        localStorage.setItem('tasksList', JSON.stringify(this.tasks));
        this.newItemText = '';
      }
    }
  },
  created() {
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
</style>
