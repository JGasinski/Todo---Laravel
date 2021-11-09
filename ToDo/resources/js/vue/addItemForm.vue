<template>
    <div class="addItem">
        <input type="text" v-model="item.name" />
        <font-awesome-icon
            icon="plus-square"
            @click="addItem()"
            :class="[ item.name ? 'active' : 'inactive', 'plus']"
        />
        
    </div>

</template>

<script>
export default {
    data: function () {
        return {
            item: {
                name:""
            }
        }
    },
    methods: {
        addItem() {
            if(this.item.name =='') {
                return;
            }

            axios.post('api/item/store', {
                item: this.item
            })
            .then(response => {
                if( response.status == 201 ) {
                    this.item.name = "";
                    this.$emit('reloadlist');
                }
            })
            .catch ( error => {
                console.log( error );
            })
        }
    }
}

</script>

<style scoped>
.addItem {
    display: flex;
    justify-content: center;
    align-items: center;
}
input {
    background: rgb(228, 236, 228);
    border: 2px;
    outline: none;
    padding: 3px;
    margin-right: 10px;
    width: 100px;
}
.plus {
    font-size: 20px;
}
.active {
    color: rgb(245, 247, 245);
}
.inactive {
    color: rgb(12, 12, 12);
}
</style>