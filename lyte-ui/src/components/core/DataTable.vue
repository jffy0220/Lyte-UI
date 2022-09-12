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
        </v-card-title>
        <v-data-table
          :headers="headers"
          :items="orders"
          :search="search"
        ></v-data-table>
      </v-card>
</template>

<script>

export default {
    name: 'DataTable',
    data: () => ({
        search: '',
        headers: [
            { text: 'Order Number', value: 'order_number' },
            { text: 'Customer Name', value: 'customer_name' }
        ],
        orders: [
            {
                order_number: 'ABC123',
                customer_name: 'Ashley Farley'
            }
        ]
    })
}

</script>