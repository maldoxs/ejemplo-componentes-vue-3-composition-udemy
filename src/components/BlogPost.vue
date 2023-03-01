<script setup>
    //defineProps(["title", "id", "body", "colorText"]);

    defineProps({
        title: String,
        id: {
            type: Number,
            default: 100,
        },
        body: {
            type: String,
            default: "Sin descripcion",
        },
    });

    //recibe un [] y dentro el nombre de la propiedad q viene desde el componente padre
    const emit = defineEmits(["cambiarFa"]);
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">{{ id }} - {{ title }}</h5>
            <p>{{ body }}</p>
            <button
                @click="emit('cambiarFa', title)"
                class="btn btn-outline-primary"
            >
                Favorito
            </button>
        </div>
    </div>
</template>
