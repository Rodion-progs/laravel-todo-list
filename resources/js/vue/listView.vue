<template>
<div>
    <list-item
        v-for="item in items"
        :key="item.id"
        :item="item"
        @itemChanged="$emit('reloadList')"

    />
</div>
</template>

<script>
import listItem from './listItem';
export default {
    name: "listVue",
    components: {
        listItem
    },
    props: {
        items: {
            type: Array,
            default: [],
        }
    }
}
</script>

<style >

</style>
