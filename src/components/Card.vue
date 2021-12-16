<template>
  <div>
    <v-container>
      <v-row>
        <v-col v-for="(client, i) in listClients" :key="i" cols="4">
          <v-card class="mx-auto" max-width="344" elevation="5" outlined>
            <v-list-item three-line>
              <v-list-item-content>
                <v-list-item-title class="text-h5 mb-1">
                  {{ client.name }}
                </v-list-item-title>
                <v-list-item-subtitle>
                  {{ client.document }}
                </v-list-item-subtitle>
                <v-list-item-subtitle>
                  {{ client.email }}
                </v-list-item-subtitle>
                <v-list-item-subtitle>
                  {{ client.celphone }}
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <v-card-actions>
              <v-btn outlined rounded text @click="edit(client)"> Editar </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "CardClient",
  data() {
    return {};
  },
  props: {
    listClients: {
      type: Array,
    },
  },
  methods: {
    edit(data) {
      this.$emit('dataToEdit',data)
    },
  },
};
</script>

<style lang="scss" scoped>
</style>