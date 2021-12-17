<template>
  <div>
    <v-container>
      <v-row>
        <v-col v-for="(item, i) in list" :key="i" cols="4">
          <v-card class="mx-auto" max-width="344" elevation="5" outlined>
            <v-list-item three-line>
              <v-list-item-content>
                <v-list-item-title class="text-h5 mb-1">
                  {{ item.name }}
                </v-list-item-title>
                <v-list-item-subtitle>
                  {{
                    item.ref
                      ? "Referencia: "
                      : item.document
                      ? "Documento: "
                      : ""
                  }}
                  {{ item.document || item.ref }}
                </v-list-item-subtitle>
                <v-list-item-subtitle>
                  {{ item.ref ? "Valor: " : item.email ? "Email: " : "" }}
                  {{ item.email || item.value }}
                </v-list-item-subtitle>
                <v-list-item-subtitle>
                  {{
                    item.stock
                      ? "Inventario: "
                      : item.celphone
                      ? "Celular: "
                      : ""
                  }}
                  {{ item.celphone || item.stock }}
                </v-list-item-subtitle>
                <v-list-item-subtitle>
                  {{ item.description ? "Descripción: " : "" }}
                  {{ item.description }}
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <v-card-actions>
              <v-btn outlined rounded text @click="edit(item)"> Editar </v-btn>
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
    return {
      title: [],
    };
  },
  props: {
    list: {
      type: Array,
    },
    view: {
      type: String,
    },
  },
  methods: {
    edit(data) {
      this.$emit("dataToEdit", data);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>