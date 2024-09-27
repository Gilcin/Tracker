<template>
    <BoxView>
        <div class="columns">
            <div class="column is-7">
                {{ tarefa.descricao || 'Tarefa sem descrição' }}
            </div>
            <div class="column">
                <CronometroView :tempoEmSegundos="tarefa.duracaoEmSegundos" />
            </div>
        </div>
    </BoxView>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import CronometroView from './CronometroView.vue';
import ITarefa from '../Interfaces/ITarefa';
import BoxView from './BoxView.vue';

export default defineComponent({
    name: 'TarefaView',
    components: {
        CronometroView,
        BoxView
    },
    props: {
        tarefa: {
            type: Object as PropType<ITarefa>,
            required: true
        }
    }
});

</script>

