<template>
    <div class="box formulario">
        <div class="columns">
            <div class="column is-8" role="form" aria-label="Formulario para criacao de uma nova tarefa">
                <input 
                type="text" 
                class="input" 
                placeholder="Qual tarefa deseja iniciar?"
                v-model="descricao"
                />
            </div>
            <div class="column">
                <TemporizadorView @finalizarTarefa="finalizarTarefa"/>
            </div>
        </div>
    </div>
</template>


<script lang="ts">
import { defineComponent } from 'vue';
import TemporizadorView from './TemporizadorView.vue';

    export default defineComponent({
        name: 'InsertFormulario',
        emits: ['aoSalvarTarefa'],
        components: {
            TemporizadorView
        },
        data() {
            return {
                descricao: ''
            }
        },
        methods: {
            finalizarTarefa(tempoDecorrido: number): void {
                this.$emit('aoSalvarTarefa', {
                    duracaoEmSegundos: tempoDecorrido,
                    descricao: this.descricao
                })
                this.descricao = ''
            }
        }
    });
</script>

<style> 
.formulario {
    color: var(--texto-primario);
    background-color: rgb(18, 229, 179); 
}
.input{
    background-color: rgba(75, 75, 75, 0.918);
}
</style>
