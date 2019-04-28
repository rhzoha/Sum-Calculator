<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase text-xs-center">
        <h4>Product Calculator</h4>
      </v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>

    <v-content>
      <v-container>
        <v-layout row wrap>
          <v-flex xs12 md6>
            <v-container grid-list-xs>
              <v-btn color="success" class="rounded full-width" v-on:click="add">Add Product</v-btn>
                <v-card v-for="(item, index) in items.slice().reverse()" :key="index" class="mt-2 rounded">
                  <v-card-text>
                    <v-text-field 
                      type="text" 
                      v-model="item.name"
                      label="Description">
                    </v-text-field>
                    <v-text-field 
                      type="number" 
                      v-model.number="item.price" 
                      label="Price"
                      >
                    </v-text-field>
                    <v-text-field 
                      type="number" 
                      v-model.number="item.quantity" 
                      min="1"
                      label="Quantity"
                      >
                    </v-text-field>
                    <v-text-field 
                      type="number" 
                      v-model.number="item.amount = item.price * item.quantity"
                      label="Amount"
                      readonly
                      >
                    </v-text-field>
                    <!-- <input type="number" v-model.number="totalItem(item)" readonly> -->
                    <v-btn 
                      v-on:click="remove(index)" 
                      color="error"
                      class="rounded" 
                      style="margin:0">Remove</v-btn>
                  </v-card-text>
                </v-card>
            </v-container>
          </v-flex>

          <v-flex xs12 md6>
            <v-container grid-list-xs class="result-display rounded">
              <v-text-field
                name="subtotal"
                label="Sub Total"
                readonly
                v-model.number="subtotal"
              ></v-text-field>
              <v-text-field
                name="discount"
                label="Discount %"
                v-model.number="discount"
              ></v-text-field>
              <v-text-field
                name="finalAmount"
                label="Final Amount"
                outline
                readonly
                v-model.number="finalAmount"
              ></v-text-field>
            </v-container>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>

export default {
  name: 'App',
  components: {
    
  },
  data () {
    return {
      //
      items: [
        {
          description: '', 
          quantity: '', 
          price: '',
          amount: ''
        }
      ],
      discount: ''
    }
  },
  methods : {
    add () {
      this.items.push({
        description: '',
        quantity: '',
        price: '',
        amount: ''
      })
    },
    remove (index) {
      this.items.splice(index, 1)
    }
  },
  computed : {
    subtotal: function() {
      let sum = 0;
      return this.items.reduce((sum, item) => sum + item.amount, 0);
    },
    finalAmount () {
      return this.subtotal - (this.subtotal * (this.discount)/100)
    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
}
.full-width {
  width: 100%;
  margin: 5px 0;
}
.rounded {
  border-radius: 10px;
}
.result-display {
  background-color: #ededed;
  margin-top: 2rem;
}
</style>
