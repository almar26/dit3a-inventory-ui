<template>
  <v-container fluid>
    <div>
      <v-card elevation="0">
        <v-card-title>
          List of Inventory
          <v-spacer></v-spacer>
          <v-spacer></v-spacer>
          <v-spacer></v-spacer>
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Search"
            single-line
            hide-details
          ></v-text-field>
        </v-card-title>
        <v-data-table :items="inventory" :headers="headers"  :search="search">
          <!-- <template v-slot:item.actions="{ item }"></template> -->
          <template slot="item.actions" scope="{ item }">
            <v-btn icon color="primary" @click="viewData(item)"
              ><v-icon>mdi-open-in-new</v-icon></v-btn
            >
            <v-btn icon color="warning"><v-icon>mdi-pencil</v-icon> </v-btn>
            <v-btn icon color="error"><v-icon>mdi-delete</v-icon> </v-btn>
          </template>
        </v-data-table>
      </v-card>
    </div>

    <!-- DIALOG BOX -->
    <v-dialog v-model="dialog" width="500">
      <v-card>
        <v-toolbar dense color="primary" class="mb-2" dark>
          <v-icon class="mr-2">mdi-menu</v-icon>
          <v-toolbar-title>{{ item_name }}</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn icon small @click="dialog = false">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </v-toolbar>
        <v-card-text>
          <!-- <p>ID: {{ id }}</p>
          <p>Item name: {{ item_name }}</p>
          <p>Category: {{ category }}</p>
          <p>Stock: {{ stock }}</p> -->
          <v-list dense>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>ID</v-list-item-title>
              </v-list-item-content>
              <v-list-item-content>
                <v-list-item-subtitle>: {{ id }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <v-divider></v-divider>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Item Name</v-list-item-title>
              </v-list-item-content>
              <v-list-item-content>
                <v-list-item-subtitle>: {{ item_name }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <v-divider></v-divider>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Category</v-list-item-title>
              </v-list-item-content>
              <v-list-item-content>
                <v-list-item-subtitle>: {{ category }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <v-divider></v-divider>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Stock</v-list-item-title>
              </v-list-item-content>
              <v-list-item-content>
                <v-list-item-subtitle>: {{ stock }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary">
            <v-icon small left>mdi-pencil</v-icon>
            Edit
          </v-btn>

          <v-btn color="error">
            <v-icon small left>mdi-delete</v-icon>
            Delete
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>
<script>
export default {
  data() {
    return {
      dialog: false,
      search: "",
      headers: [
        {
          text: "ID",
          align: "start",
          sortable: false,
          value: "id",
        },
        { text: "Item", value: "item_name", sortable: false },
        { text: "Category", value: "category", sortable: false },
        { text: "Stock", value: "stock", sortable: false },
        { text: "", value: "actions", align: "end" },
      ],
      inventory: [
        {
          id: 1,
          item_name: "Linen Paper",
          category: "Raw Materials",
          stock: 463,
        },
        {
          id: 2,
          item_name: "Computer Paper",
          category: "Finished Good",
          stock: 403,
        },
      ],

      id: 0,
      item_name: "",
      category: "",
      stock: 0,
    };
  },

  methods: {
    viewData(item) {
      console.log(item);
      this.id = item.id;
      this.item_name = item.item_name;
      this.category = item.category;
      this.stock = item.stock;
      this.dialog = true;
    },
  },
};
</script>