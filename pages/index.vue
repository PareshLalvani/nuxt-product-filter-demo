<template>
  <div>
    <v-row class="mt-10">
      <v-col cols="6"></v-col>
      <v-col cols="2">
        <v-select
          :items="colors"
          v-model="color"
          label="Color"
          dense
        ></v-select>
      </v-col>
      <v-col cols="2">
        <v-select
          :items="sizeList"
          v-model="size"
          label="Size"
          dense
        ></v-select>
      </v-col>
      <v-col cols="2">
        <v-btn depressed dark @click="applyFilter"> {{ filterName }} </v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="4" v-for="(product, i) in products" :key="i">
        <v-card class="mx-auto" max-width="344">
          <v-carousel height="150" :show-arrows="false">
            <v-carousel-item
              v-for="(variation, j) in product.variation"
              :key="j"
            >
              <v-sheet :color="variation.color" height="100%">
                <v-row
                  class="fill-height"
                  align="center"
                  justify="center"
                ></v-row>
              </v-sheet>
            </v-carousel-item>
          </v-carousel>

          <v-card-title>
            {{ product.name }}
          </v-card-title>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      color: "",
      size: "",
      colors: ["indigo", "deep-purple", "pink"],
      sizeList: ["Small", "Medium", "Large"],
      productList: [
        {
          id: 1,
          name: "Product 1",
          variation: [
            {
              size: "Small",
              color: "indigo",
            },
            {
              size: "Medium",
              color: "deep-purple",
            },
            {
              size: "Large",
              color: "pink",
            },
          ],
        },
        {
          id: 2,
          name: "Product 2",
          variation: [
            {
              size: "Medium",
              color: "deep-purple",
            },
            {
              size: "Large",
              color: "pink",
            },
          ],
        },
        {
          id: 3,
          name: "Product 3",
          variation: [
            {
              size: "Small",
              color: "indigo",
            },
            {
              size: "Large",
              color: "pink",
            },
          ],
        },
        {
          id: 4,
          name: "Product 4",
          variation: [
            {
              size: "Small",
              color: "indigo",
            },
          ],
        },
        {
          id: 5,
          name: "Product 5",
          variation: [
            {
              size: "Large",
              color: "pink",
            },
          ],
        },
      ],
      display: "allProducts",
      filterName: "Apply Filter",
    };
  },
  computed: {
    products() {
      return this[this.display];
    },
    allProducts() {
      return this.productList;
    },
    filterdProducts() {
      let filterColor = this.color,
        filterSize = this.size;
      return this.productList.filter(function (product) {
        let filtered = true;
        if (filterColor) {
          filtered = product.variation.some(function (e) {
            return e.color === filterColor;
          });
        }
        if (filtered && filterSize) {
          filtered = product.variation.some(function (e) {
            return e.size === filterSize;
          });
        }
        return filtered;
      });
    },
  },
  methods: {
    applyFilter() {
      if (!this.size && !this.color) return;
      if (this.filterName == "Apply Filter") {
        this.display = "filterdProducts";
        this.filterName = "Reset Filter";
      } else {
        this.filterName = "Apply Filter";
        this.display = "allProducts";
        this.size = "";
        this.color = "";
      }
    },
  },
};
</script>
