<template>
  <div>
    <v-container>
      <v-row>
        <v-col>
          <form @submit.prevent="submit">
            <v-text-field
              v-model="name"
              :counter="10"
              label="Name"
              required
            ></v-text-field>

            <v-text-field
              v-model="document"
              :counter="10"
              label="Documento"
              required
              type="number"
            ></v-text-field>

            <v-text-field
              v-model="phoneNumber"
              :counter="7"
              label="Phone Number"
              required
              type="number"
            ></v-text-field>

            <v-text-field
              v-model="email"
              label="E-mail"
              required
            ></v-text-field>

            <v-btn class="mr-4" type="submit"> submit </v-btn>
            <!-- <v-btn @click="clear"> clear </v-btn> -->
          </form>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { clients } from "@/mock/Moks";
export default {
  data() {
    return {
      name: "asd",
      phoneNumber: null,
      email: "asdas",
      idClient: null,
      document: null,
      id: null
    };
  },
  props: {
    newClient: {
      type: Boolean,
      default: false,
    },
    editDataClient: {
      type: Boolean,
      default: false,
    },
    dataEdit: {
      type: Object,
    }
  },
  created() {
    // console.log(clients);
    console.log("this.newClient", this.newClient);
    if (this.newClient) {
      this.name = "";
      this.phoneNumber = null;
      this.email = "";
      this.document = null;
    }
    if (this.editDataClient) {
      this.id = this.dataEdit.id;
      this.name = this.dataEdit.name;
      this.phoneNumber = this.dataEdit.celphone;
      this.email = this.dataEdit.email;
      this.document = this.dataEdit.document;
    }
  },
  methods: {
    submit() {
      if (this.newClient) {
        this.createClient();
      } else if (this.editDataClient) {
        this.editData();
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
      this.$emit('reloadCard');
    },
    editData() {
      clients.data.map(client => {
        if (client.id === this.id) {
          client.name = this.name,
          client.document = this.document,
          client.celphone = this.phoneNumber,
          client.email = this.email
        }
      })
      this.$emit('reloadCard');

    }
  },
};
</script>

<style lang="scss" scoped>
</style>