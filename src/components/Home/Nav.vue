<template>
    <v-container>
        <v-app-bar app color="primary" dark>
            <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
            <v-toolbar-title>BOOK_AUTH_REVIEWS</v-toolbar-title>
        </v-app-bar>

            <v-navigation-drawer
                app
                v-model="drawer"
                clipped-left
                color="primary white--text"

            >
            Joy Joy
                
            </v-navigation-drawer>
       
    </v-container>

</template>
<script>

export default {
    name: "Nav",
    data(){
        return{
            drawer:false,
        }
    },
}
</script>
