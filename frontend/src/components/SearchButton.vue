<template>
    <div class="search">
        <form class="d-flex">
            <input v-model="searchText" type="text" placeholder="Search..." class="form-control">
            <button class="btn btn-outline-success" v-on:click.prevent="searchArticles">Search</button>
        </form>
    </div>
</template>

<script>
    export default {
        name: 'SearchButton',
        data: function () {
            return {
                searchText: '',
            }
        },
        methods: {
            searchArticles() {
                const text = this.searchText.trim();
                if (text.charAt(0) !== '') {
                    this.$router.push({name: 'Home', query: {search: text}})
                }
            }
        },
    }
</script>


<style scoped>
</style>