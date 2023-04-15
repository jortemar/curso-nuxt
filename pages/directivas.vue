<template>
    <div>
        <p>{{ message }}</p>
        <p v-show="true">Este texto se muestra en función del parámetro de v-show</p>
        <p v-if="num > 10">Este texto con v-if hace lo mismo, pero no se renderiza si no se muestra</p>
        <p v-else>Si no salta el v-if, lo hace este texto con v-else</p>
        <ul>
            <li v-for="item in items" :key="item">{{ item }}</li>
        </ul>
        <input v-model="name" type="text" />
        {{ name }}
        {{ nameReverser }}
        <span tag="tag is-warning">
            {{ error }}
        </span>
        <button @click="saludo" class="button is-info">
            Saluda
        </button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            message: "Hola OpenWebinars",
            num: 5,
            items: [1,2,3,4,5,6],
            name: '',
            error: ''
        }
    },

    computed: {
        nameReverser() {
            return this.name.split('').reverse().join('')
        }
    },

    watch: {
        name() {
            if (this.name.length > 5) {
                this.error = 'Nombre demasiado largo'
            } else {
                this.error = ''
            }
        }
    },

    methods: {
        saludo() {
            console.log(`Hola ${this.name}`) 
        }
    }
}
</script>

