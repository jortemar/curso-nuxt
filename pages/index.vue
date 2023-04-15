<template>
  <div>
    <!-- esto es para el slot -->
    <Hero @onShowBanner="changeShowBannerValue">
      <Banner slot="header" style="width: 790px" v-if="showBanner" />
      <Slogan slot="header" style="width: 790px" v-else />
    </Hero>

    <div class="container">
      <section class="section">
        <div class="columns is-multiline">
          <restaurant-card 
          :name="restaurant.name"
          :description="restaurant.description"
          :category="restaurant.category"
          :slug="restaurant.slug"
          :likes="restaurant.likes"
          :image="restaurant.image"
          @onLikeButton="sumLikes(restaurant)"
          v-for="(restaurant, index) in restaurants" :key="index"
          class="restaurant-card"
        />
        </div>   
      </section>
    </div>
    
  </div>
</template>

<script>
// En Nuxt no es necesario importar los componentes ni declararlos.
// Lo estoy haciendo por seguir el curso tal cual, pero esto hay que quitarlo
import RestaurantCard from '../components/RestaurantCard.vue'
import Hero from '../components/Hero'
import Banner from '../components/Banner'
import Slogan from '../components/Slogan'
import api from '@/services/api'

export default {
  components: {
    RestaurantCard,
    Hero,
    Banner,
    Slogan
  },
  async asyncData() {
    try {
      const { data } = await api.getRestaurants()
      return { restaurants: data }
    } catch {
      return { restaurants: [] }
    }
  },

  // async created() {
  //   const response = await api.getRestaurants()
  //   if (response.status == 200) {
  //     this.restaurants = response.data
  //   }
  // },

  data() {
    return {
      showBanner: false,
      restaurants: []
    }
  },  

  methods: {
    async sumLikes(restaurant) {
      const payload = {
        id: restaurant.id,
        data: {
          likes: restaurant.likes++
        }
      }
      const response = await api.putSumRestaurantLikes(payload)
      console.log(response)
      if(response.status == 200) {
        restaurant.likes++
      }
    },
    changeShowBannerValue() {
      this.showBanner = !this.showBanner
    }
  },

  name: 'IndexPage'
}
</script>

<style scoped>
.restaurant-card {
  margin: 10px 10px;
  max-width: 300px;
}
</style>
