<template>
    <div class="box has-text-weight-bold">
        <slot>  </slot>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'BoxView'
});

</script>

<style scoped>
    .box {
        background-color: rgb(27, 202, 182);
        color: var(--texto-primario);
        font-size: 18px;
    }
    .box:hover {
        background-color: rgb(2, 156, 120);
        transition: .5s;
    }
</style>