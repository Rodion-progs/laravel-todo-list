<template>
    <div class="container">
        <div class="header">
            <h2 class="header__title">Title</h2>
            <add-item-form @reloadList="getList"/>
            <list-view :items="items" @reloadList="getList"/>
        </div>
    </div>
</template>

<script>
import addItemForm from './addItemForm';
import listView from './listView';
export default {
    name: "App",
    components: {
        addItemForm,
        listView,
    },
    data() {
        return {
            items: []
        }
    },
    created() {
        this.getList();
    },
    methods: {
        getList () {
            axios.get('api/items')
            .then(res => {
                this.items = res.data;
            })
            .catch( e => {
                console.log(e)
            } )
        }
    }
}
</script>

<style>
.container {
    width: 90%;
    max-width: 500px;
    margin: auto;
    padding: 0 10px;
}
.header {
    background-color: #e6e6e6;
    padding: 10px;
}
.header__title {

}
</style>
