<script setup>
    defineProps(['title','id','body'])
    //const emit = defineEmits([cambiarFavorito])
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">{{id}} - {{title}}</h5>
            <p>{{body}}</p>
            <button class="btn btn-outline-primary" @click="$emit('cambiarFavorito',title)">Favorito</button>
        </div>
    </div>
</template>