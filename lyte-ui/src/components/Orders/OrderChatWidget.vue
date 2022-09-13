<template>
    <v-list three-line>
        <template v-for="(item, index) in items">
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
        ]
    })
}
</script>