<template>
    <div class="item">
        <input
            type="checkbox"
            @change="updateCheck()"
            v-model="item.completed"
            />
            <span :class="[item.completed ? 'completed' : '', 'item.text']"> {{ item.name }} </span>
            <button @click="removeItem()" class="trashcan" >
                <font-awesome-icon icon="trash" />
            </button>
    </div>
</template>

<script>
export default {
    props: ['item'],
    methods: {
        updateCheck() {
            axios.put('api/item/' + this.item.id, {
                item: this.item
            })
            .then( resonse => {
                if( resonse.status == 200 ) {
                    this.$emit('itemchanged');
                }
            })
            .catch( error => {
                console.log( error );
            })
        },
        removeItem() {
            axios.delete('api/item/' + this.item.id )
            .then( response => {
                if( response.status == 200 ) {
                    this.$emit('itemchanged');
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
.completed {
    text-decoration: line-through;
    color: rgb(247, 10, 10);
}
.itemText {
    width: 100%;
    margin-left: 20px;
}
.item {
    display: flex;
    justify-content: left;
    align-items: center;
}
.trashcan {
    background: rgb(217, 243, 217);
    border: none;
    color: rgb(218, 45, 45);
    outline: none;
}
</style>