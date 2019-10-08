<template>
  <div class="page">
    <div v-if="$apollo.loading">Loading...</div>
    <!-- Begin editing your homepage here -->
    <div v-if="!hasPageData">
      <content-hero-banner
        id="hero-banner"
        backgroundImgUrl="https://www.bl.uk/britishlibrary/~/media/bl/global/language%20of%20birds/africangrey-thinkstockphotos-533333167.jpg"
        backgroundAltTag="A bird"
        :title="name"
        ctaText="Shop for Stuff"
        ctaUrl="/shop"
        :ctaHandler="() => { this.$router.push('/shop') }"
      />
      <nacelle-products :handle="'stuff'">
          <template v-slot:default="{ product }">
              <product-details :product="product" />
          </template>
      </nacelle-products>
      <content-side-by-side
        imageUrl="https://www.wonderopolis.org/wp-content/uploads/2012/09/Macaws-shutterstock_9273904.jpg"
        ctaText="Buy Stuff"
        ctaUrl="/shop"
        backgroundColor="#f2eee8"
        :ctaHandler="() => { this.$router.push('/shop') }"
      />
      <content-side-by-side
        imageUrl="https://www.allaboutbirds.org/guide/assets/og/75221611-1200px.jpg"
        ctaText="Buy Stuff"
        ctaUrl="/shop"
        backgroundColor="#f2eee8"
        :reverseDesktop="true"
        :ctaHandler="() => { this.$router.push('/shop') }"
      />
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import { getPage } from '@nacelle/nacelle-graphql-queries-mixins'
import ProductDetails from '~/components/ProductDetails'

export default {
  data() {
    return {
      handle: 'homepage'
    }
  },
  mixins: [getPage],
  components: {
    ProductDetails
  },
  computed: {
    ...mapState('space', ['name']),
    hasPageData() {
      if (this.page) {
        if (
          this.page.sections &&
          this.page.sections.length > 0
        ) {
          return true
        }

        if (
          this.page.fields &&
          this.page.fields.body
        ) {
          return true
        }

        return false
      }
    }
  }
}
</script>

<style scoped>
  .product-data-load {
    margin: 50px;
  }
</style>
