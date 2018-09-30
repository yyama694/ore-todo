<template>
    <div>
        <h1>Todo List</h1>
        <input type="text" v-model="newTask">
        <input type="button" value="追加" v-on:click="addTask">
        <div class="list">
            <ul>
                <li v-for="item in list" :key="item.id">
                    <span :class="{ complete: item.isComplete }">{{ item.value }}　</span>
                    <input type="button" value="達成" v-on:click="item.isComplete=true"> 
                    <input type="button" value="削除"> 
                </li>
            </ul>
        </div>
    </div>
</template>
    
<script>
export default {
    data() {
        return {
            list: [
               { id:1, value: "たまご買う", isComplete: false }, 
               { id:2, value: "図書館に本を返す", isComplete: false },
               { id:3, value: "宅急便を受け取る", isComplete: false }
            ],
            newTask: "",
            nextId: 4
        }
    },
    methods : {
        addTask() {
            if(!this.newTask.trim()) {
                return
            }
            this.list.push({
                id: this.nextId++,
                value: this.newTask,
                isComplete: false 
            })
            this.newTask = ""
        },
    }
}
</script>

<style scoped>
.list{
    width: 60%;
    margin: auto;
    text-align: left;
}
.complete{
    text-decoration: line-through;
}
</style>