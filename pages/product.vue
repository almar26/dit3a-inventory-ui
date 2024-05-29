<template>
  <v-container fluid>
    <div class="mb-4">
      <v-btn color="primary" @click="dialog = true">Add Record</v-btn>
    </div>
    <div>
      <v-card elevation="0">
        <v-card-title>
          List of Products
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
        <v-data-table :items="productList" :headers="headers" :search="search">
          <!-- <template v-slot:item.actions="{ item }"></template> -->
          <template slot="item.actions" scope="{ item }">
            <v-btn icon color="primary" @click="viewData(item)"
              ><v-icon>mdi-open-in-new</v-icon></v-btn
            >
            <v-btn icon color="warning" @click="getUpdateData(item)"><v-icon>mdi-pencil</v-icon> </v-btn>
            <v-btn icon color="error" @click="deleteRecordDialog(item.id)"><v-icon>mdi-delete</v-icon> </v-btn>
          </template>
        </v-data-table>
      </v-card>
    </div>

    <!-- ADD RECORD DIALOG BOX -->
    <v-dialog v-model="dialog" width="400">
      <v-card>
        <v-card-text>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field
              v-model="product_code"
              :rules="productCodeRules"
              label="Product Code"
            ></v-text-field>

            <v-text-field
              v-model="product_name"
              :rules="productNameRules"
              label="Product Name"
            ></v-text-field>

            <v-text-field
              v-model="product_description"
              :rules="productDescriptionRules"
              label="Product Description"
            ></v-text-field>

            <v-text-field v-model="category"
            :rules="productCategoryRules"
             label="Category"></v-text-field>
            <v-text-field
              type="number"
              :rules="quantityRules"
              v-model="quantity"
              label="Quantity"
            ></v-text-field>
          </v-form>
        </v-card-text>
        <v-card-actions class="pb-5">
          <v-btn color="primary" @click="addRecord">Add Record</v-btn>
          <v-spacer></v-spacer>
          <v-btn color="error" @click="dialog = false">Cancel</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <!-- VIEW DIALOG BOX -->
    <v-dialog persistent v-model="viewDialog" width="500">
      <v-card>
        <v-toolbar dense color="primary" class="mb-2" dark>
          <v-icon class="mr-2">mdi-menu</v-icon>
          <v-toolbar-title>{{ product_name }}</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn icon small @click="viewDialog = false">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </v-toolbar>
        <v-card-text>
          <v-list dense>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Product Code</v-list-item-title>
              </v-list-item-content>
              <v-list-item-content>
                <v-list-item-subtitle>: {{ product_code }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <v-divider></v-divider>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Product Name</v-list-item-title>
              </v-list-item-content>
              <v-list-item-content>
                <v-list-item-subtitle>: {{ product_name }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <v-divider></v-divider>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Product Description</v-list-item-title>
              </v-list-item-content>
              <v-list-item-content>
                <v-list-item-subtitle>: {{ product_description }}</v-list-item-subtitle>
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
                <v-list-item-title>Quantity</v-list-item-title>
              </v-list-item-content>
              <v-list-item-content>
                <v-list-item-subtitle>: {{ quantity }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" @click="getUpdateData(update_record)">
            <v-icon small left>mdi-pencil</v-icon>
            Edit
          </v-btn>

          <v-btn color="error" @click="deleteRecordDialog(product_id)">
            <v-icon small left>mdi-delete</v-icon>
            Delete
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <!-- UPDATE RECORD DIALOG BOX -->
    <v-dialog v-model="updateDialog" width="400">
      <v-card>
        <v-toolbar dense color="primary" class="mb-2" dark>
          <v-icon class="mr-2">mdi-menu</v-icon>
          <v-toolbar-title>Update Record</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn icon small @click="updateDialog = false">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </v-toolbar>
        <v-card-text>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field
              v-model="product_code"
              :rules="productCodeRules"
              label="Product Code"
            ></v-text-field>

            <v-text-field
              v-model="product_name"
              :rules="productNameRules"
              label="Product Name"
            ></v-text-field>

            <v-text-field
              v-model="product_description"
              :rules="productDescriptionRules"
              label="Product Description"
            ></v-text-field>

            <v-text-field v-model="category"
            :rules="productCategoryRules"
             label="Category"></v-text-field>
            <v-text-field
              type="number"
              :rules="quantityRules"
              v-model="quantity"
              label="Quantity"
            ></v-text-field>
          </v-form>
        </v-card-text>
        <v-card-actions class="pb-5">
          <v-btn color="primary" @click="updateRecord">Update Record</v-btn>
          <v-spacer></v-spacer>
          <v-btn color="error" @click="updateDialog = false">Cancel</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>


    <!-- DELETE DIALOG BOX -->
    <v-dialog v-model="deleteDialog" width="300">
      <v-sheet
      class="px-7 pt-7 pb-4 mx-auto text-center d-inline-block"
      color="blue-grey darken-3"
      dark
    >
      <div class="grey--text text--lighten-1 text-body-2 mb-4">
        Are you sure you want to delete this record?
      </div>

      <v-btn
        class="ma-1"
        color="grey"
        plain
        @click="deleteDialog = false"
      >
        Cancel
      </v-btn>

      <v-btn
        class="ma-1"
        color="error"
        plain
        @click="deleteRecord"
      >
        Delete
      </v-btn>
    </v-sheet>
    </v-dialog>

    <!-- SNACKBAR -->
      <!-- Add Record snackbar-->
      <v-snackbar v-model="snackbar" color="success" top right>
        Successfully Created!
        <template v-slot:action="{ attrs }">
          <v-btn icon v-bind="attrs" @click="snackbar = false">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </template>
      </v-snackbar>

       <!-- update record snackbar -->
    <v-snackbar v-model="updateSnackbar" color="green" top right>
      Successfully updated!
      <template v-slot:action="{ attrs }">
        <v-btn icon v-bind="attrs" @click="updateSnackbar = false">
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </template>
    </v-snackbar>

      <!-- Delete record snackbar -->
    <v-snackbar v-model="deleteSnackbar" color="green" top right>
      Successfully deleted record!
      <template v-slot:action="{ attrs }">
        <v-btn icon v-bind="attrs" @click="deleteSnackbar = false">
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </template>
    </v-snackbar>
  </v-container>
</template>

<script>
export default {
  name: "InspirePage",
  data() {
    return {
      snackbar: false,
      deleteSnackbar: false,
      updateSnackbar: false,
      valid: true,
      product_id: null,
      product_code: "",
      product_name: "",
      product_description: "",
      category: "",
      quantity: 0,
      dialog: false,
      viewDialog: false,
      deleteDialog: false,
      updateDialog: false,
      search: "",
      headers: [
        {
          text: "Product Code",
          align: "start",
          sortable: false,
          value: "attributes.product_code",
        },
        {
          text: "Product Name",
          value: "attributes.product_name",
          sortable: false,
        },
        {
          text: "Product Description",
          value: "attributes.product_description",
          sortable: false,
        },
        {
          text: "Category",
          value: "attributes.product_category",
          sortable: false,
        },
        {
          text: "Quantity",
          value: "attributes.product_quantity",
          sortable: false,
        },
        { text: "", value: "actions", align: "end" },
      ],
      productCodeRules: [(v) => !!v || "Product Code is required"],
      productNameRules: [(v) => !!v || "Product Name is required"],
      productDescriptionRules: [(v) => !!v || "Product Description is required"],
      quantityRules: [(v) => !!v || "Quantity is required"],
      productCategoryRules: [(v) => !!v || "Category is required"],

      productList: [],
      update_record: {}
    };
  },

  mounted() {
    this.getProductList();
  },

  methods: {
    getProductList() {
      this.$axios
        .get("/api/product-tables")
        .then((response) => {
          console.log(response);
          this.productList = response.data.data;
        })
        .catch((error) => {
          console.log("error");
        });
    },

    viewData(item) {
      console.log(item);
      this.update_record = item;
      this.product_id = item.id;
      this.product_code = item.attributes.product_code;
      this.product_name = item.attributes.product_name;
      this.product_description = item.attributes.product_description;
      this.category = item.attributes.product_category;
      this.quantity = item.attributes.product_quantity;
      this.viewDialog = true;
    },

    getUpdateData(item) {
      
      this.product_id = item.id;
      this.product_code = item.attributes.product_code;
      this.product_name = item.attributes.product_name;
      this.product_description = item.attributes.product_description;
      this.category = item.attributes.product_category;
      this.quantity = item.attributes.product_quantity;
      this.updateDialog = true;
    },
 

    addRecord() {
      if (this.$refs.form.validate()) {
        let payload = {
          data: {
            product_code: this.product_code,
            product_name: this.product_name,
            product_description: this.product_description,
            product_category: this.category,
            product_quantity: this.quantity,
          },
        };
        this.$axios
          .post("/api/product-tables", payload)
          .then((response) => {
            console.log(response);
            this.$refs.form.reset();
            this.getProductList();
            this.snackbar = true;
           
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },

    updateRecord() {
      if (this.$refs.form.validate()) {
        let payload = {
          data: {
            product_code: this.product_code,
            product_name: this.product_name,
            product_description: this.product_description,
            product_category: this.category,
            product_quantity: this.quantity,
          },
        };

        this.$axios
          .put(`/api/product-tables/${this.product_id}`, payload)
          .then((response) => {
            console.log(response);
            //this.$refs.form.reset();
            this.getProductList();
            this.updateSnackbar = true;
           
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },

    deleteRecordDialog(id) {
      console.log(id)
      this.product_id = id;
      this.deleteDialog = true;
    },

    deleteRecord() {
      this.$axios.delete(`/api/product-tables/${this.product_id}`)
      .then(response => {
        console.log(response);
        this.deleteSnackbar = true;
        this.getProductList();
        this.deleteDialog = false
        this.viewDialog = false;
      })
      .catch(error => {
        console.log(error);
      })
    }

  },

  computed: {},
};
</script>