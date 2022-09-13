<template>
    <v-card>
        <v-card-title class="text-center justify-center py-6">
            <h5 class="font-weight-bold text-h5">Order KPI</h5>
        </v-card-title>

        <v-tabs
            v-model="tab"
            background-color="transparent"
            color="non-tab"
            grow
        >
            <v-tab v-for="item in items" :key="item">
                {{ item }}
            </v-tab>

            <v-tabs-items v-model="tab">
                <v-tab-item v-for="item in items" :key="item">
                    <v-card color="basil" flat>
                        <v-card-text>{{ text }}</v-card-text>
                    </v-card>
                </v-tab-item>
            </v-tabs-items>
        </v-tabs>
    </v-card>
</template>

<script>
export default {
    name: 'OrderBasicMetricWidget',
    data: () => ({
        tab: null,
        items: [ 'Orders by Day', 'Orders by Week', 'Orders by Month', 'Order Fulfillment Rate'],
        text: 'Testing!'
    })
}
</script>

<style scoped>
.non-tab {
    background-color: #fffbe6 !important;
}
</style>