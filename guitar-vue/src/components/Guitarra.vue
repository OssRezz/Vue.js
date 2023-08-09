<script setup>

const props = defineProps({
    guitarraProps: {
        type: Object,
        required: true
    }
});
defineEmits(['agregar-carrito']);

</script>

<template>
    <div class="col-md-6 col-lg-4 my-4 row align-items-center">
        <div class="col-4">
            <img class="img-fluid" :src="`/img/${guitarraProps.imagen}.jpg`" :alt="`imagen guitarraProps ${guitarraProps.nombre}`">
        </div>
        <div class="col-8">
            <h3 class="text-black fs-4 fw-bold text-uppercase">{{ guitarraProps.nombre }}</h3>
            {{ numero }}
            <p>{{ guitarraProps.descripcion }}</p>
            <p class="fw-black text-primary fs-3">{{ guitarraProps.precio }}</p>
            <button type="button" class="btn btn-dark w-100" @click="$emit('agregar-carrito', guitarraProps)">
                Agregar al Carrito
            </button>
        </div>
    </div><!-- FIN GUITARRA -->
</template>

<style></style>