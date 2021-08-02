 <template>
  <div class="home">
    <section class="hero is-medium is-dark mb-5">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">
          Welcome to The Online Store
        </p>
        <p class="subtitle">
          The best sports apparel online store
        </p>
      </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">Latest Products</h2>
      </div>

      <ProductBox  v-for="product in latestProducts" v-bind:key="product.id" v-bind:product="product"/>
      
    </div>

    this is a vue test
  </div>
</template>

<script>
import axios from 'axios'
import ProductBox from '@/components/ProductBox'

export default {
  name: 'Home',
  data(){
    return{
      latestProducts: []
    }
  },
  components: {
    ProductBox
  },
  mounted(){
    this.getLatestProducts()

    document.title = 'Home | Online Store'
  },
  methods: {
    async getLatestProducts(){
      this.$store.commit('setIsLoading', true)

      await axios.get('/api/v1/latest-products/')
      .then(response => {
        this.latestProducts = response.data
      })
      .catch(error => {
        console.log(error)
      })
      this.$store.commit('setIsLoading', false)
    }
  }
}
</script>



