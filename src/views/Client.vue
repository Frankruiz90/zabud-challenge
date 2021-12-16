<template>
  <div :key="carList">
    <card-client :listClients="listClients" @dataToEdit="dataToEdit($event)" />
    <form-client
      v-if="crateNewClient || editData"
      :newClient="crateNewClient"
      :dataEdit="dataSelected"
      :editDataClient="editData"
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
import { clients } from "@/mock/Moks";
import CardClient from "../components/Card.vue";
import FormClient from "../components/Form.vue";
export default {
  data() {
    return {
      listClients: [],
      crateNewClient: false,
      carList: 0,
      editData: false,
      dataSelected: {},
      form: 0,
    };
  },

  created() {
    this.listClients = [...clients.data];
  },
  components: {
    CardClient,
    FormClient,
  },
  methods: {
    newClient() {
      this.form += 1;
      this.crateNewClient = true;
      this.editData = false;
    },
    newList() {
      this.listClients = [...clients.data];
    },
    dataToEdit(event) {
      this.form += 1;
      this.crateNewClient = false;
      this.editData = true;
      this.dataSelected = event;
    },
  },
};
</script>

<style lang="scss" scoped>
</style>