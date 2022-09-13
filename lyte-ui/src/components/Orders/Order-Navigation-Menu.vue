<template>
    <div>
        <v-list>
            <v-list-item>
                <v-list-item-title>Navigation Submenu</v-list-item-title>
            </v-list-item>

            <v-list-group :value="false" prepend-icon="mdi-account-circle">
                <template v-slot:activator>
                    <v-list-item-title>Order Management</v-list-item-title>
                </template>

                <v-list-group :value="false" no-action sub-group>
                    <template v-slot:activator>
                        <v-list-item-content>
                            <v-list-item-title>View Order KPI Dashboard</v-list-item-title>
                        </v-list-item-content>
                    </template>
                </v-list-group>
            </v-list-group>
        </v-list>
    </div>
</template>

<script>
export default {
    name: 'OrderNavigationMenu',
    data: () => ({
        admins: [
            ['Management', 'mdi-account-multiple-outline']
        ]
    })
}
</script>