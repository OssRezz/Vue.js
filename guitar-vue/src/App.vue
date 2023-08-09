<script setup>
import { ref, watch, onMounted } from 'vue';
import { db } from './data/guitarras';
import GuitarraComponent from './components/Guitarra.vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';

const guitarras = ref([]);
const carrito = ref([]);
const guitarra = ref({});

watch(carrito, () => {
    guardarLocalStorage();
}, {
    deep: true
});

onMounted(() => {
    guitarras.value = db;
    guitarra.value = db[3];

    const carritoStorage = localStorage.getItem('carrito');
    if (carritoStorage) {
        carrito.value = JSON.parse(carritoStorage);
    }
});

const guardarLocalStorage = () => {
    localStorage.setItem('carrito', JSON.stringify(carrito.value));
}

const agregarCarrito = (guitarra) => {
    const ValidateGuitarra = carrito.value.findIndex((e) => e.id == guitarra.id);
    if (ValidateGuitarra >= 0) {
        return carrito.value[ValidateGuitarra].cantidad++;
    }
    guitarra.cantidad = 1;
    carrito.value.push(guitarra);

    guardarLocalStorage();
};

const aumentarCarrito = (id) => {
    const ValidateGuitarra = carrito.value.findIndex((e) => e.id == id);
    carrito.value[ValidateGuitarra].cantidad++;
};

const descontarCarrito = (id) => {
    const ValidateGuitarra = carrito.value.findIndex((e) => e.id == id);
    if (carrito.value[ValidateGuitarra].cantidad <= 1) return
    carrito.value[ValidateGuitarra].cantidad--;
};

const eliminarCarrito = (id) => {
    carrito.value = carrito.value.filter((producto) => producto.id != id);
}

const vaciarCarrito = () => {
    carrito.value = [];
}

</script>

<template>
    <Header :carrito="carrito" :guitarra="guitarra" @descontar-carrito="descontarCarrito"
        @aumentar-carrito="aumentarCarrito" @eliminar-Carrito="eliminarCarrito" @agregar-Guitarra="agregarCarrito"
        @vaciar-Carrito="vaciarCarrito" />

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
            <GuitarraComponent v-for="guitarra in guitarras" :key="guitarra.id" :guitarraProps="guitarra"
                @agregar-carrito="agregarCarrito" />
        </div>
    </main>

    <Footer />
</template>