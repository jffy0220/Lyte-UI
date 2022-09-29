<template>
    <v-list three-line>
        <template v-for="(item, index) in orderMessages">
            <v-subheader v-if="item.header" :key="item.header" v-text="item.header"></v-subheader>
            <v-divider v-else-if="item.divider" :key="index" :inset="item.inset"></v-divider>
            <v-list-item
                v-else
                :key="item.title"
            >
                <v-list-item-content>
                    <v-list-item-title v-html="item.title"></v-list-item-title>
                    <v-list-item-subtitle v-html="item.subtitle"></v-list-item-subtitle>
                </v-list-item-content>
            </v-list-item>
        </template>
    </v-list>
</template>

<script>
export default {
    name: 'OrderChatWidget',
    data: () => ({
        items: [
            { header: 'Today' },
            {
                title: 'ABC123',
                subtitle: `<span class="text--primary">Ashley Farley</span> &mdash; Order Proccessed - 09/13/2022 08:00:00AM`
            }
        ],
        orderMessages: []
    }),
    created() {
        fetch(`http://localhost:3000/order-messages`)
            .then(async response => {
                const order_messages = await response.json();
                console.log(order_messages);
                let header = { header: 'Today' }
                this.orderMessages.push(header);
                for (let i = 0; i < order_messages.length; i++) {
                    fetch(`http://localhost:3000/order/${order_messages[i].order_id}`)
                        .then(async order_response => {
                            const order = await order_response.json()
                            let obj = {
                                title: order.order_number,
                                subtitle: `<span class="text--primary">${order_messages[i].employee_name}</span> &mdash; ${order_messages[i].message} - ${order_messages[i].date_created}`
                            }
                            this.orderMessages.push(obj)
                        })
                }
            })
    }
}
</script>