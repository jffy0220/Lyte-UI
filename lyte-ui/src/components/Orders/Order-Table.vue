<template>
    <v-card>
        <v-card-title>
          Orders
          <v-spacer></v-spacer>
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Search"
            single-line
            hide-details
          ></v-text-field>
            <v-dialog
              v-model="dialog"
              fullscreen
              hide-overlay
              transition="dialog-bottom-transition"
          >
              <template v-slot:activator="{ on, attrs }">
                  <v-btn color="primary" dark v-bind="attrs" v-on="on">Create New Order</v-btn>
              </template>
              <v-card>
                  <v-toolbar dark color="primary">
                      <v-btn icon dark @click="dialog = false">
                          <v-icon> mdi-close</v-icon>
                      </v-btn>
                      <v-toolbar-title>Settings</v-toolbar-title>
                      <v-spacer></v-spacer>
                      <v-toolbar-items>
                          <v-btn dark text @click="dialog = false">
                              Create Order
                          </v-btn>
                      </v-toolbar-items>
                  </v-toolbar>
                  Hello World!
              </v-card>
          </v-dialog>
        </v-card-title>
        <v-data-table
          :headers="headers"
          :items="orders"
          :search="search"
        >
        </v-data-table>
        
      </v-card>
</template>

<script>


export default {
  components: {  },
    name: 'OrderTable',
    data: () => ({
        search: '',
        dialog: false,
        headers: [
          { text: 'Order Number', value: 'order_number' },
          { text: 'First Name', value: 'customer_first_name' },
          { text: 'Last Name', value: 'customer_last_name' },
          { text: 'Order Type', value: 'order_type_name' },
          { text: 'Order Status', value: 'order_status_name' },
          { text: 'Quantity', value: 'order_line_item_qty' },
          { text: 'Value', value: 'order_purchase_value' },
          { text: 'Delivery City', value: 'customer_city' },
          { text: 'Delivery State', value: 'customer_state' },
          { text: 'Delivery Ccountry', value: 'customer_country' }
        ],
        items: [
          { order_number: 'ABC123', customer_name: 'Justin Farley' },
          { order_number: 'DEF456', customer_name: 'Ashley Farley' }
        ],
        orders: []
    }),
    created() {
      fetch("http://localhost:3000/order")
        .then(async response => {
          const data = await response.json();

          if (!response.ok) {
            const error = (data && data.message) || response.statusText;
            return Promise.reject(error);
          }

          console.log(data);

          for (let i = 0; i < data.length; i++) {
            let obj = {
              order_number: data[i].order_number,
              order_id: data[i].id,
              order_type_id: data[i].order_type_id,
              order_status_id: data[i].order_status_id,
              customer_first_name: '',
              customer_last_name: '',
              customer_id: '',
              order_type_name: '',
              order_status_name: '',
              order_line_item_qty: 'TESTING VALUE FOR NOW',
              order_purchase_value: 'TESTING VALUE FOR NOW',
              customer_city: '',
              customer_state: '',
              customer_country: ''
            }

            fetch(`http://localhost:3000/customer/${data[i].customer_id}`)
              .then(async res_customer => {
                const customer_data = await res_customer.json();
                console.log(customer_data);
                obj.customer_first_name = customer_data[0].first_name;
                obj.customer_last_name = customer_data[0].last_name;
                obj.customer_id = customer_data[0].id;
                obj.customer_city = customer_data[0].address[0].city;
                obj.customer_state = customer_data[0].address[0].state;
                obj.customer_country = customer_data[0].address[0].country;

                fetch(`http://localhost:3000/order-type/${obj.order_type_id}`)
                  .then(async res_order_type => {
                    const order_type_data = await res_order_type.json();
                    obj.order_type_name = order_type_data.name;

                    fetch(`http://localhost:3000/order-type-status/${obj.order_status_id}`)
                      .then(async res_order_type_status => {
                        const order_type_status_data = await res_order_type_status.json();
                        obj.order_status_name = order_type_status_data.name;
                      })
                  })
              })
            this.orders.push(obj);
          }
        })
    }
}

</script>