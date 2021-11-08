<template>
    <div class="addItem">
        <input type="text"  v-model="item.name" />
        <font-awesome-icon
            icon="plus-square"
            @click="addItem()"
            :class="[ item.name ? 'active' : 'inactive', 'plus' ]"
        />
    </div>
</template>

<script>
export default {
    data: function() {
        return {
            item: {
                name:""
            }
        }
    },
    methods: {
        addItem() {
            if( this.item.name == ''){
                return;
            }

            axios.post('api/item/store', {
                item: this.item
            })
            .then( response => {
                if( response.status == 201 ) {
                    this.item.name == "";
                }
            })
            .catch( error => {
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
    background: rgb(250, 249, 248);
    border:0 px;
    outline: none;
    padding: 3px ;
    margin-right: 10;
    width: 100%;
}
.plus {
    font-size: 25px;
}
.active {
    color: rgb(5, 5, 5);

}

.inactive {
    color: rgb(86, 202, 86);
}

</style>