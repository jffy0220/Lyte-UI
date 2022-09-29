<template>
    <v-dialog
        v-model="dialog"
        fullscreen
        hide-overlay
        transition="dialog-bottom-transition"
    >
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
</template>

<script>
export default {
    name: 'NewOrderDialog',
    data: () => ({
        dialog: false
    })
}
</script>