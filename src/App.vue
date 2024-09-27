<template>
  <main class="columns is-gapless is-multiline" :class="{ 'dark': modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema"/>
    </div>
    <div  class="column is-three-quarter conteudo">
        <InsertFormulario @aoSalvarTarefa="salvarTarefa"/>
        <div class="lista">
          
          <TarefaView v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa"/>
          <BoxView v-if="listaEstaVazia">
          Você não esta muito produtivo hoje :(
        </BoxView>
        </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import InsertFormulario from './components/InsertFormulario.vue';
import TarefaView from './components/TarefaView.vue';
import ITarefa from './Interfaces/ITarefa';
import BoxView from './components/BoxView.vue';


export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    InsertFormulario,
    TarefaView,
    BoxView
  },
  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false
    }
  },
  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length === 0
    }
  },
  methods: {
    salvarTarefa (tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    },
    trocarTema (modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo
    }
  }
});
</script>

<style>
  .lista {
    padding: 1.25rem;
  }
  main {
    --bg-primario: rgb(215, 236, 255);
    --texto-primario: #000000;
  }
  main.dark {
    --bg-primario: #2b2d42;
    --texto-primario: #ffffff;
  }

  .conteudo {
    background-color: var(--bg-primario);
  }
</style>
