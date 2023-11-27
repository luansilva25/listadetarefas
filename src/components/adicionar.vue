<template>
  <div class="add">
    <input
      type="text"
      v-model="tarefa"
      id="tarefa"
      placeholder="Qual tarefa que deseja realizar?"
    />
    <input
      type="button"
      value="adicionar"
      :key="tarefa"
      @click="add"
      id="add"
    />
  </div>
  <div class="tarefas">
    <h1>tarefas a serem realizadas</h1>
    <div v-for="(tarefa, index) in tarefas" :key="index" class="aguarde">
      <p v-if="editar !== index">{{ tarefa }}</p>
      <input
        v-else
        type="text"
        placeholder="Nova tarefa"
        v-model="tarefas[index]"
      />
      <div class="interacao">
        <input v-if="editar !== index" type="button" value="✏️" @click="edicao(index)" />
        <input v-else type="button" value="💾" @click="salvar">
        <input
          type="button"
          :key="index"
          @click="finalizar(index)"
          id="finalizar"
          value="✓"
        />
       
        <input
          type="button"
          value="X"
          @click="removerTarefa(index)"
          id="remover"
        />
      </div>
    </div>
  </div>
  <div class="finalizados">
    <h1>finalizados</h1>
    <div class="finalizado" v-for="finalizado in finalizados" :key="index">
      <p>{{ finalizado }}</p>
      <input type="button" value="🗑️" @click="removerFinalizado(index)" />
    </div>
  </div>
</template>
<script>
export default {
  name: "adicionar",
  data() {
    return {
      tarefas: [],
      tarefa: "",
      finalizados: [],
      finalizado: "",
      editar: -1,
    };
  },
  methods: {
    add: function () {
      if (this.tarefa === "") {
        alert("adicione algo");
      } else {
        this.tarefas.push(this.tarefa);
        this.tarefa = "";
      }
    },
    finalizar: function (index) {
      this.finalizados.push(this.tarefas[index]);
      this.tarefas.splice(index, 1);
    },
    removerTarefa: function (index) {
      this.tarefas.splice(index, 1);
      let removertarefa = document.querySelector(".aguarde");
      removertarefa.style.display = "none";
    },
    removerFinalizado: function (index) {
      this.finalizados.splice(index, 1);
      let removerfinalizado = document.querySelector(".finalizado");
      removerfinalizado.style.display = "none";
    },
    edicao: function (index) {
      this.editar = index;
    },
    salvar: function () {
      this.editar = -1;
    },
  },
};
</script>
<style>
.add {
  display: flex;
  height: 500px;
  align-items: start;
  justify-content: center;
  flex-direction: column;
  gap: 10px;
  width: 400px;
}
#tarefa {
  width: 250px;
  outline: 0;
  border: none;
  border-bottom: 1px solid gray;
}
#tarefa:focus,
#tarefa:hover {
  border-bottom: 1px solid cornflowerblue;
}
#add {
  width: 100px;
  height: 30px;
  background-color: cornflowerblue;
  color: white;
}
.tarefas {
  display: flex;
  flex-direction: column;
  height: 500px;
  width: 500px;
}
.tarefas h1 {
  text-align: center;
}
.aguarde {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 70px;
  width: 400px;
  box-shadow: 1px 2px 2px 1px rgba(0, 0, 0, 0.58);
  padding: 10px;
  gap: 10px;
}
#finalizar {
  background-color: rgb(0, 255, 0);
  color: white;
}
#remover {
  background-color: red;
  color: white;
}
.interacao {
  display: flex;
  gap: 10px;
}
.interacao input {
  width: 30px;
  height: 30px;
}
.finalizados {
  height: 500px;
  width: 400px;
}
.finalizados h1 {
  text-align: center;
}
.finalizado {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 70px;
  width: 400px;
  box-shadow: 1px 2px 2px 1px rgba(0, 0, 0, 0.58);
  margin-left: 10px;
  padding: 10px;
}
.finalizado input {
  width: 30px;
  height: 30px;
  background-color: red;
  color: white;
}
</style>
