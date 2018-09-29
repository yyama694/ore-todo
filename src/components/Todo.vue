<template>
    <div>
        <h1>Todo List</h1>
        <input type="text" v-model="newTask">
        <input type="button" value="追加" v-on:click="addTask">
        <div class="list">
            <ul>
                <li v-for="item in list" :key="item.id">
                    {{ item.value }}　
                    <input type="button" value="達成"> <!-- ここを追加 -->
                    <input type="button" value="削除"> <!-- ここを追加 -->
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
               { id:1, value: "たまご買う" },
               { id:2, value: "図書館に本を返す" },
               { id:3, value: "宅急便を受け取る" }
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
                value: this.newTask
            })
            this.newTask = ""
        }
    }
}
</script>

<style scoped>
.list{
    width: 60%;
    margin: auto;
    text-align: left;
}
</style>