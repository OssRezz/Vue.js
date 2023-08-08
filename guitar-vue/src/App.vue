<script setup>
import { ref, reactive, onMounted } from 'vue';
import { db } from './data/guitarras';
import Guitarra from './components/Guitarra.vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';
const guitarras = ref([]);
const carrito = ref([]);
const guitarra = ref({});

onMounted(() => {
    guitarras.value = db;
    guitarra.value = db[3];
});

const agregarCarrito = (guitarra) => {
    const ValidateGuitarra = carrito.value.findIndex((e) => e.id == guitarra.id);
    if (ValidateGuitarra >= 0) {
        return carrito.value[ValidateGuitarra].cantidad++;
    }
    guitarra.cantidad = 1;
    carrito.value.push(guitarra);
};

const aumentarCarrito = (id) => {
    const ValidateGuitarra = carrito.value.findIndex((e) => e.id == id);
    return carrito.value[ValidateGuitarra].cantidad++;
};

const descontarCarrito = (id) => {
    const ValidateGuitarra = carrito.value.findIndex((e) => e.id == id);
    if (carrito.value[ValidateGuitarra].cantidad <= 1) return
    return carrito.value[ValidateGuitarra].cantidad--;
};

const eliminarCarrito = (id) => {
    const ArrayGuitars = carrito.value.filter((e) => e.id != id);
    console.log(ArrayGuitars);
    return carrito.value = [ArrayGuitars];
}



</script>

<template>
    <Header :carrito="carrito" :guitarra="guitarra" @descontar-carrito="descontarCarrito"
        @aumentar-carrito="aumentarCarrito" @eliminar-Carrito="eliminarCarrito" @agregar-Guitarra="agregarCarrito" />

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
            <Guitarra v-for="guitarra in guitarras" :guitarra="guitarra" @agregar-carrito="agregarCarrito" />
        </div>
    </main>

    <Footer />
</template>