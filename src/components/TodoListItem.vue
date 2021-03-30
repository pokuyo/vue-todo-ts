<template>
    <li>
        <span 
            class="item" 
            :class="todoItemClass" 
            @click="toggleItem"
        >{{ todoItem.title }}</span>
        <button @click="removeItem">삭제</button>
    </li>
</template>

<script lang="ts">
    import { Todo } from '@/App.vue'
    import Vue,{ PropType } from 'vue'

    export default Vue.extend({
        props: {
            todoItem: Object as PropType<Todo>,
            index: Number
        },
        methods: {
            toggleItem() {
                this.$emit('toggle', this.todoItem, this.index);
            },
            removeItem() {
                this.$emit('remove', this.index);
            }
        },
        computed: {
            //extend 사용 시 computed에 return type 명시 필요
            todoItemClass():string | null {
                return this.todoItem.done ? 'complete' : null
            }
        }
    })
</script>

<style scoped>
.item {
    cursor: pointer;
}
.complete {
    text-decoration: line-through;
}
</style>