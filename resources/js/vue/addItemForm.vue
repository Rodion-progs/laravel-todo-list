<template>
    <div class="addItem">
        <input
            type="text"
            class="addItem__input"
            v-model="item.name"
            placeholder="Item"/>
        <div class="buttons">
            <VueButton
                class="button-primary buttons__button"
                :class="buttonClass"
                :disabled="!item.name"
                @click="addItem"
            >Add</VueButton>
            <VueButton
                class="button-danger buttons__button"
                :class="buttonClass"
                :disabled="!item.name"
                @click="clearInput"
            >Clear</VueButton>
        </div>
    </div>
</template>

<script>
import VueButton from './interface/vue-button';
export default {
    name: "addItemForm",
    components: {VueButton},
    data () {
        return {
            item: {
                name: ""
            }
        }
    },
    computed: {
        buttonClass() {
            return !this.item.name ? 'buttons__button-inactive' : null;
        }
    },
    methods: {
        clearInput() {
            this.item.name = ""
        },
        addItem() {
            if (this.item.name === "") return
            axios.post('api/item/store', {
                item: this.item
            })
            .then(res => {
                if ( res.status === 201) {
                    this.clearInput();
                }
                this.$emit('reloadList')
            })
            .catch(e => {
                console.log(e);
            })
        }
    }
}
</script>

<style>
.addItem {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
}
.addItem__input {
    flex-grow: 1;
    margin-right: 10px;
    padding: 5px 10px;
    border-radius: 5px;
    outline: none;
    border: 1px solid #45454550;
    background-color: #f7f7f7;
}
.buttons {
    margin: 0 -5px;
}
.buttons__button {
    margin-right: 5px;
    margin-left: 5px;
    flex-grow: 1;
}
.buttons__button-inactive {
    opacity: 0.5;
    cursor: not-allowed;
}
</style>
