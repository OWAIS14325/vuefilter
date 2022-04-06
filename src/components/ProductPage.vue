<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col col-3">
        <side-bar :filters="filters" @update-filters="showProducts($event)" />
      </div>
      <div class="col col-9">
        <div class="row">
          <div
            class="col col-4"
            v-for="(product, index) in products"
            :key="index"
          >
            <div class="card" style="width: 18rem">
              <img
                class="card-img-top"
                :src="product.image"
                alt="Card image cap"
              />
              <div class="card-body">
                <h5 class="card-title">{{ product.name }}</h5>
                <p class="card-text">
                  {{ product.description }}
                </p>
                <h6>{{ product.price }}</h6>
                <p>{{ product.product_category }}</p>
                <a href="#" class="btn btn-primary">Buy Now</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import SideBar from "@/components/SideBar.vue";
export default {
  name: "ProductPage",
  components: {
    SideBar,
  },
  data() {
    return {
      apiData: [],
      displayProduct: [],
    };
  },
  computed: {
    filters() {
      return this.apiData.filters;
    },
    products() {
      return this.displayProduct;
    },
  },
  async created() {
    const response = await fetch(
      "https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=&sort_dir=desc&filter="
    );
    const data = await response.json();
    this.apiData = data.result;
    this.displayProduct = this.apiData.products;
    console.log(this.apiData);
  },
  methods: {
    showProducts(filters) {
      if (filters.length) {
        let a = [];
        for (let i = 0; i < filters.length; ++i) {
          const data = this.apiData.products.filter((product) => {
            if (product[filters[i].code] !== filters[i].value) return false;

            return true;
          });
          a = [...a, ...data]
        }
        this.displayProduct = a
      } else{
        this.displayProduct = this.apiData.products
      }
    },
  },
};
</script>