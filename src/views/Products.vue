<template>
  <div :key="carList">
    <card-client
      :list="listProducts"
      :view="view"
      @dataToEdit="dataToEdit($event)"
    />
    <form-client
      v-if="newProduct || editData"
      :newProduct="newProduct"
      :dataEdit="dataSelected"
      :editDataProduct="editData"
      @reloadCard="newList()"
      :key="form"
    />
    <v-tooltip top>
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          class="mx-2 mb-2"
          fab
          dark
          color="indigo"
          absolute
          right
          bottom
          outlined
          @click="newClient()"
          v-bind="attrs"
          v-on="on"
        >
          <v-icon dark> mdi-plus </v-icon>
        </v-btn>
      </template>
      <span>Agregar cliente</span>
    </v-tooltip>
  </div>
</template>

<script>
import { productsList } from "@/mock/MoksProducts";
import CardClient from "../components/Card.vue";
import FormClient from "../components/Form.vue";
export default {
  data() {
    return {
      listProducts: [],
      newProduct: false,
      carList: 0,
      editData: false,
      dataSelected: {},
      form: 0,
      view: "products",
    };
  },

  created() {
    this.listProducts = [...productsList.data];
  },
  components: {
    CardClient,
    FormClient,
  },
  methods: {
    newClient() {
      this.form += 1;
      this.newProduct = true;
      this.editData = false;
    },
    newList() {
      this.listProducts = [...productsList.data];
    },
    dataToEdit(event) {
      this.form += 1;
      this.newProduct = false;
      this.editData = true;
      this.dataSelected = event;
    },
  },
};
</script>

<style lang="scss" scoped>
</style>