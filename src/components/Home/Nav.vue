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
            <v-list>
                
            <v-list-item-group  >
                <v-list-item  v-for="(item, i) in items" :key="i" :to="item.link"  >
                    <v-list-item-icon>
                        <v-icon class="white--text">{{ item.icon }}</v-icon>
                    </v-list-item-icon>
                    <v-list-item-content class="white--text">{{ item.text }}</v-list-item-content>
                 </v-list-item>
            </v-list-item-group>
                
            </v-list>   
                
            </v-navigation-drawer>
       
    </v-container>

</template>
<script>

export default {
    name: "Nav",
    data(){
        return{
            drawer:false,
            items :[
                {text:'Books', link:'/', icon:'mdi-home'},
                {text:'Authors', link:'/authors', icon:'mdi-book'},
                {text:'Reviews', link:'/reviews', icon:'mdi-home'},
            ]
        }
    },
}
</script>
