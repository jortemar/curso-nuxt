<template>
    <div>
        <h2 class="title is-2">FoodAdvisor, tu web de restaurantes</h2>
        <div class="subcribe" v-if="!is_subscribed">
            <input v-model="email" type="text" class="input email" placeholder="email..." />
            <button class="button is-info" @click="subscribe">
                Suscribirse
            </button>
        </div>
    </div>
</template>

<script>
import api from '../services/api';

export default {
    data() {
        return {
            email: '',
            is_subscribed: false
        }
    },

    methods: {
        async subscribe() {
            const payload = {
                email: this.email
            }
            const response = await api.postSubscribeUser(payload)
            if (response.status == 201) { // 201 : Created
                this.is_subscribed = true
            }
        }
    }
}
</script>

<style scoped>
.subcribe {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}

.email {
    width: 80%;
}
</style>