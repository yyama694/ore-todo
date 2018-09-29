<template>
    <div>
        <h1>Todo List</h1>
        <input type="text">
        <input type="button" value="追加">
        <div class="list">
            <ul>
                <li v-for="item in list" :key="item.id">{{ item.value }}</li>
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
            ]
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