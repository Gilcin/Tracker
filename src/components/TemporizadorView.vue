<template>
     <div class="is-flex is-align-items-center is-justify-content-space-between">
                <CronometroView :tempoEmSegundos="tempoEmSegundos"/>
                <button class="button" @click="iniciar" :disabled="cronometroRodando">
                    <span class="icon">
                        <i class="fas fa-play"></i>
                    </span>
                    <span>play</span>
                </button>
                <button class="button" @click="finalizar" :disabled="!cronometroRodando">
                    <span class="icon">
                        <i class="fas fa-stop"></i>
                    </span>
                    <span>stop</span>
                </button>
                </div>
</template>

<script lang="ts">
    import { defineComponent } from 'vue';
    import CronometroView from './CronometroView.vue';

    export default defineComponent({
        name: 'TemporizadorView',
        components: {
            CronometroView
        },
        data() {
          return {
              tempoEmSegundos: 0,
              cronometro: 0,
              cronometroRodando: false
          }  
        },
        methods: {
    iniciar() {
        this.cronometroRodando = true;
        this.cronometro = setInterval(() => {
            this.tempoEmSegundos += 1;
        }, 1000);
    },
    finalizar() {
        // Garantir que o tempo correto seja emitido
        const tempoFinalizado = this.tempoEmSegundos; // Armazena o valor antes de resetar

        // Emitir o tempo decorrido antes de qualquer reset
        this.$emit('finalizarTarefa', tempoFinalizado);

        // Limpa e reseta o cronômetro
        this.cronometroRodando = false;
        clearInterval(this.cronometro);
        this.tempoEmSegundos = 0; // Reseta após emitir o evento
    }
}

    });
</script>