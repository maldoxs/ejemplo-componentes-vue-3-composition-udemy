<script setup>
    defineProps(["inicio", "fin", "totalArreglo"]);
    const emit = defineEmits(["siguiente", "anterior"]); //para eventos personalisados

    const activarSiguiente = () => {
        emit("siguiente");
    };
</script>

<template>
    total arreglo = {{ totalArreglo }}
    <div class="btn-group" role="group" aria-label="Basic example">
        <button
            @click="emit('anterior')"
            type="button"
            class="btn btn-primary"
            :disabled="inicio === 0"
        >
            Previus {{ inicio }}
        </button>
        <button
            @click="activarSiguiente"
            type="button"
            class="btn btn-primary"
            :disabled="fin >= totalArreglo"
        >
            Next {{ fin }}
        </button>
    </div>
</template>
