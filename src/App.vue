<template>
  <div id="todo">
    <div class="container mt-5">
      <div class="row justify-content-md-center">
        <div class="col-md-8 bg-white p-3">
          <h1 class="text-center">Bienvenue dans l'application Todo de {{ name }} !</h1>
          <p>Ceci est un exemple de contenu pour tester l'affichage de votre application.</p>
          <hr>

          <!-- Modifications -->
          <div class="d-flex align-items-center py-2">
            <input v-model="newItemText" class="form-control flex-grow-1">
            <button class="btn btn-primary ms-2" v-on:click="addNewToDO">Ajouter</button>
          </div>

          <hr>
          <div class="d-flex align-items-center justify-content-between px-3 py-2" v-for="t in hiddentasks" :key="t.task">
            <div>{{ t.task }}</div>
            <div>
              <input type="checkbox" v-model="t.completed" class="form-check-input" />
              {{ t.completed }}
            </div>
            
          </div>
          <div class="d-flex flex-row-reverse justify-content-between">
            
            <input type="checkbox" v-model="hide" class="form-check-input">
            <label><span class="badge bg-primary">Afficher/Cacher les tasks accomplis</span> </label>


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
      tasks: [
        { "task": "Acheter du pain", "completed": false },
        { "task": "Aller à la gym", "completed": false },
        { "task": "Envoyer les emails", "completed": false },
        { "task": "Préparer la réunion de demain", "completed": false },
        { "task": "Appeler le plombier", "completed": false },
        { "task": "Planifier les vacances", "completed": false },
        { "task": "Mettre à jour le CV", "completed": false },
        { "task": "Réparer la bicyclette", "completed": false },
        { "task": "Lire le rapport", "completed": false },
        { "task": "Nettoyer le garage", "completed": false }
      ],
      hide: true
    };
  },
  computed: {
    hiddentasks() {
      return this.hide ? this.tasks.filter(t => !t.completed) : this.tasks
    }
  }
};
</script>

<style>
html body {
  background-color: rgb(247, 208, 208);
  margin: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
