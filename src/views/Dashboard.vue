<template>
  <div>
    <div class="dashboard">
      <div class="container is-login" v-if="id">
        <div class="col-md-3">
          <SideInfo :name="user.name" />
        </div>
        <div class="col-md-9">
          <div class="carousel">
            <Carousel />
          </div>
          <div class="special-categories">
            <SpecialCategory />
          </div>
          <CardDiscountRow />
          <ButtonCategories />
          <div class="card-categories">
            <h2>Paling Banyak Dicari</h2>
            <CardCategories />
          </div>
          <PromoRow />
          <CardProductRow />
        </div>
      </div>
      <div class="container" v-else>
        <div class="col-md-12">
          <div class="carousel">
            <Carousel />
          </div>
          <div class="special-categories">
            <SpecialCategory />
          </div>
          <CardDiscountRow />
          <ButtonCategories />
          <div class="card-categories">
            <h2>Paling Banyak Dicari</h2>
            <CardCategories />
          </div>
          <PromoRow />
          <CardProductRow />
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
import { mapActions, mapState } from 'vuex';
import SideInfo from '@/components/templates/SideInfo.vue';
import ButtonCategories from '@/components/templates/ButtonCategories.vue';
import CardProductRow from '@/components/templates/CardProductRow.vue';
import CardCategories from '@/components/templates/CardCategories.vue';
import SpecialCategory from '@/components/SpecialCategory.vue';
import Carousel from '@/components/Carousel.vue';
import CardDiscountRow from '@/components/templates/CardDiscountRow.vue';
import PromoRow from '../components/templates/PromoRow.vue';
import Footer from '../components/footer.vue';

export default {
  name: 'Home',
  components: {
    ButtonCategories,
    CardProductRow,
    CardCategories,
    SpecialCategory,
    Carousel,
    CardDiscountRow,
    PromoRow,
    Footer,
    SideInfo,
  },
  data() {
    return {
      id: null,
    };
  },
  computed: {
    ...mapState('user', ['user']),
  },
  created() {
    this.id = localStorage.getItem('id');
    this.getUserId();
  },
  mounted() {
    this.getUserById();
  },
  methods: {
    ...mapActions('user', ['getUserById']),
    ...mapActions('user', ['getUserId']),
    ClickCategory() {
      const submenu = document.querySelector('.submenu-category');
      submenu.classList.toggle('subcat-show');
    },

    ClickCart() {
      console.log('hello');
      const subCartLayer = document.querySelector('.submenu-icon-group');
      subCartLayer.classList.toggle('submenuCartShow');
      const cartIcon = document.querySelector('.submenu-cart-icon');
      cartIcon.classList.toggle('SubCartTop');
    },
  },
};
</script>

<style lang="scss" scoped>
  .dashboard{
    margin: 50px auto;
  }
  .is-login{
    display: flex;
    align-items: flex-start;
  }
  .container{
    padding-top: 100px;
    margin: 0 auto;
  }
  .special-categories, .carousel{
    padding: 0 5px;
    margin-bottom: 32px;
  }
  .card-categories h2{
    padding: 0 5px;
    font-weight: 700;
    font-size: 20px;
  }
  .col-md-3{
    position: relative;
    top: 50px;
  }
</style>
