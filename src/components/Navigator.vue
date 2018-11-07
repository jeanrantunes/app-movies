<template>
    <v-navigation-drawer
        v-model="drawer"
        absolute
        dark
        temporary
    >
        <v-list v-if="favorites.length > 0" class="pa-1">
            <v-list-tile v-for="item in favorites" v-bind:key="item.id">
                <v-list-tile-content>
                    <v-list-tile-title>{{item.title}}</v-list-tile-title>
                </v-list-tile-content>
            </v-list-tile>
        </v-list>
        <p v-else class="title">Não existem favoritos!</p>
    </v-navigation-drawer>
</template>
<script>
export default {
    name: "Navigator",
    data() {
        return {
            drawer: false,
            favorites: []
        }
    },
    methods: {
        show(favorites) {
            this.drawer = true,
            this.favorites = favorites
        }
    }
}
</script>
<style>

</style>

