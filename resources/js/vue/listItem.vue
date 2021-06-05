<template>
<div class="item">
    <label>
        <input
            type="checkbox"
            @change="updateCheck"
            :value="item.completed"
            class="item__checkbox"
        >
        <span class="item__text" :class="[item.completed ? 'item__text_completed' : '']">{{ item.name }}</span>
    </label>
    <VueButton
        class="button-danger item__remove"
        @click="removeItem"
        :disabled="disabled"
    >Remove</VueButton>
</div>
</template>

<script>
import VueButton from './interface/vue-button';

export default {
    name: "listView",
    props: {
        item: {
            type: Object,
            required: true
        }
    },
    components: {
      VueButton
    },
    data() {
        return {
            completed: false,
            disabled: false
        }
    },
    created() {
        this.completed = this.item.completed;
    },
    methods: {
        updateCheck() {
            if (this.disabled) return
            this.disabled = true;
            axios.put('api/item/' + this.item.id, {
                item: {...this.item, completed: !this.item.completed},
            })
            .then(res => {
                if (res.status === 200) {
                    this.$emit('itemChanged');
                }
            })
            .catch(e => {
                console.log(e);
            })
            .finally(() => {
                this.disabled = false;
            })
        },
        removeItem() {
            if (this.disabled) return
            this.disabled = true;
            axios.delete('api/item/' + this.item.id)
                .then(res => {
                    if ( res.status === 200) {
                        this.$emit('itemChanged');
                    }
                })
                .catch(e => {
                    console.log(e);
                })
                .finally(() => {
                    this.disabled = false;
                })
        }
    }
}
</script>

<style >
.item {
    background-color: #e6e6e6;
    padding: 10px 0;
    display: flex;
    align-items: center;
}
.item__text {
    font-size: 18px;
}
.item__text_completed {
    text-decoration: line-through;
    color: #999999;
}
.item__remove {
    padding: 5px;
    font-size: 14px;
    margin-left: auto;
}
.item__checkbox {
    width: 0;
    height: 0;
    overflow: hidden;
    visibility: hidden;
}
</style>
