<template>
  <div class="mb-8">
    <v-container>
      <v-row>
        <v-col>
          <v-card class="pa-3">
            <form @submit.prevent="submit">
              <v-text-field
                v-model="name"
                :counter="10"
                label="Name"
                required
              ></v-text-field>

              <v-text-field
                v-if="editDataClient || newClient"
                v-model="document"
                :counter="10"
                label="Documento"
                required
                type="number"
              ></v-text-field>
              <v-text-field
                v-if="editDataClient || newClient"
                v-model="phoneNumber"
                :counter="7"
                label="Phone Number"
                required
                type="number"
              ></v-text-field>

              <v-text-field
                v-if="editDataClient || newClient"
                v-model="email"
                label="E-mail"
                required
              ></v-text-field>

              <v-text-field
                v-if="editDataProduct || newProduct"
                v-model="ref"
                :counter="10"
                label="Referencia"
                required
                type="text"
              ></v-text-field>
              <v-text-field
                v-if="editDataProduct || newProduct"
                v-model="value"
                :counter="10"
                label="Valor"
                required
                type="number"
              ></v-text-field>
              <v-text-field
                v-if="editDataProduct || newProduct"
                v-model="stock"
                :counter="10"
                label="Inventario"
                required
                type="number"
              ></v-text-field>
              <v-text-field
                v-if="editDataProduct || newProduct"
                v-model="description"
                :counter="10"
                label="Descripción"
                required
                type="text"
              ></v-text-field>

              <v-btn class="mr-4" type="submit"> submit </v-btn>
            </form>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { clients } from "@/mock/Moks";
import { productsList } from "@/mock/MoksProducts";
export default {
  data() {
    return {
      name: "",
      phoneNumber: null,
      email: "",
      idClient: null,
      document: null,
      id: null,
      ref: "",
      value: null,
      stock: null,
      description: "",
    };
  },
  props: {
    newClient: {
      type: Boolean,
      default: false,
    },
    newProduct: {
      type: Boolean,
      default: false,
    },
    editDataClient: {
      type: Boolean,
      default: false,
    },
    editDataProduct: {
      type: Boolean,
      default: false,
    },
    dataEdit: {
      type: Object,
    },
  },
  created() {
    if (this.newClient) {
      this.name = "";
      this.phoneNumber = null;
      this.email = "";
      this.document = null;
    } else if (this.editDataClient) {
      this.id = this.dataEdit.id;
      this.name = this.dataEdit.name;
      this.document = this.dataEdit.document;
      this.phoneNumber = this.dataEdit.celphone;
      this.email = this.dataEdit.email;
    } else if (this.editDataProduct) {
      this.id = this.dataEdit.id;
      this.name = this.dataEdit.name;
      this.ref = this.dataEdit.ref;
      this.value = this.dataEdit.value;
      this.stock = this.dataEdit.stock;
      this.description = this.dataEdit.description;
    }
  },
  methods: {
    submit() {
      if (this.newClient) {
        this.createClient();
      } else if (this.editDataClient) {
        this.editData();
      } else if (this.newProduct) {
        this.createProduct();
      } else if (this.editDataProduct) {
        this.editProduct();
      }
    },
    createClient() {
      this.idClient = clients.data.length + 1;
      clients.data.push({
        id: this.idClient,
        name: this.name,
        document: this.document,
        celphone: this.phoneNumber,
        email: this.email,
      });
      this.$emit("reloadCard");
    },
    editData() {
      clients.data.map((client) => {
        if (client.id === this.id) {
          (client.name = this.name),
            (client.document = this.document),
            (client.celphone = this.phoneNumber),
            (client.email = this.email);
        }
      });
      this.$emit("reloadCard");
    },
    createProduct() {
      this.idClient = productsList.data.length + 1;
      productsList.data.push({
        id: this.idClient,
        name: this.name,
        ref: this.ref,
        value: this.value,
        stock: this.stock,
        description: this.description,
      });
      this.$emit("reloadCard");
    },
    editProduct() {
      productsList.data.map((porduct) => {
        if (porduct.id === this.id) {
          (porduct.name = this.name),
            (porduct.ref = this.ref),
            (porduct.value = this.value),
            (porduct.stock = this.stock),
            (porduct.description = this.description);
        }
      });
      this.$emit("reloadCard");
    },
  },
};
</script>

<style lang="scss" scoped>
</style>