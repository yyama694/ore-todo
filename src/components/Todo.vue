<template>
    <div>
        <h1>Todo List</h1>
        <el-input ref="new_task" class="task-input" placeholder="追加するタスクを入力してください。" v-model="newTask" @keydown.enter.native="addTask"></el-input>
        <el-button type="primary" plain @click="addTask">追加</el-button>
        <el-table
            :data="list"
            stripe
            class="list"
            row-class-name="todo-row">
            <el-table-column style="padding: 8px">
                <template slot-scope="scope">
                    <span :class="{ complete: scope.row.isComplete }">{{ scope.row.value }}</span>
                </template>
            </el-table-column>
            <el-table-column>
                <template slot-scope="scope">
                    <el-button @click="scope.row.isComplete=true" type="primary" plain size="small" v-if="!scope.row.isComplete">達成</el-button>
                    <el-button @click="scope.row.isComplete=false" type="primary" plain size="small" v-if="scope.row.isComplete">戻す</el-button>
                    <el-button @click="deleteTask(scope)" type="danger" plain size="small">削除</el-button>
                </template>
            </el-table-column>
        </el-table>
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
    methods: {
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
        deleteTask(scope) {
            // TR タグを全て取得
            const els = document.getElementsByClassName('todo-row')
            
            // 削除ボタンが押された行に deleting クラスを追加
            els[scope.$index].classList.add('deleting')

            // this を別変数で保管
            const self = this

            // setTimeout に渡す関数を定義
            const f = function() { 
                // list から 削除する要素を削除
                self.list = self.list.filter(e => e !== scope.row)
                
                // 全ての TR タグから deleting クラスを削除
                for(var i=0; i < els.length; i++){
                    els[i].classList.remove('deleting');
                }
            }

            // 0.5 秒後に削除を実施する
            setTimeout(f, 500);
        }
    },
    mounted: function() {
        this.$refs.new_task.focus()
    } 
}
</script>

<style scoped>
.list {
    width: 80%;
    margin: auto;
    text-align: left;
}
.complete {
    text-decoration: line-through;
}
h1 {
    position: relative;
    line-height: 1.4;
}
h1:before { 
    font-family: "Font Awesome 5 Free";
    content: "\f00c";
    font-size: 0.7em;
    left: 0;
    top: 0;
    color: #5ab9ff;
}
.task-input {
    width: 60%;
}
.list >>> td {
    padding: 5px;
}
@keyframes fadeout {
  0% { opacity: 1; }
  100% { opacity: 0; }
}
.list >>> .deleting {
    animation: fadeout 0.5s ease 0s forwards;
}
</style>