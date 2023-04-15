<template>
  <div>
    <!-- esto es para el slot -->
    <Hero @onShowBanner="changeShowBannerValue">
      <Banner slot="header" style="width: 790px" v-if="showBanner" />
      <Slogan slot="header" style="width: 790px" v-else />
    </Hero>

    <div class="container">
      <section class="section">
        <restaurant-card 
          :name="restaurant.name"
          :description="restaurant.description"
          :category="restaurant.category"
          :slug="restaurant.slug"
          :likes="restaurant.likes"
          @onLikeButton="sumLikes(index)"
          v-for="(restaurant, index) in restaurants" :key="index"
        />
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

  async created() {
    const response = await api.getRestaurants()
    if (response.status == 200) {
      this.restaurants = response.data
    }
  },

  data() {
    return {
      showBanner: false,
      restaurants: []
    }
  },  

  methods: {
    sumLikes(index) {
      this.restaurants[index].likes++
    },
    changeShowBannerValue() {
      this.showBanner = !this.showBanner
    }
  },

  name: 'IndexPage'
}
</script>

<!-- <style scoped>
.Banner {
  width: 790px;
}

.Slogan {
  width: 790px;
}
</style> -->
