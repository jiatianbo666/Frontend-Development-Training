<script setup>
import { ref } from 'vue'

// 待办事项数据
const todos = ref([
  { id: 1, text: '去图书馆学习' },
  { id: 2, text: '上羽毛球课' },
  { id: 3, text: '会议室开会' }
])

// 新待办事项输入
const newTodo = ref('')

// 下一个ID
const nextId = ref(4)

// 添加待办事项
const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({
      id: nextId.value++,
      text: newTodo.value.trim()
    })
    newTodo.value = ''
  }
}

// 删除单个待办事项
const deleteTodo = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id)
}

// 清空所有待办事项
const clearAll = () => {
  todos.value = []
}

// 处理Enter键提交
const handleKeyPress = (event) => {
  if (event.key === 'Enter') {
    addTodo()
  }
}
</script>

<template>
  <div class="todo-app">
    <div class="container">
      <h1 class="title">本周待办事项</h1>
      
      <!-- 待办事项列表 -->
      <div class="todo-list">
        <div 
          v-for="todo in todos" 
          :key="todo.id" 
          class="todo-item"
        >
          <span class="todo-text">{{ todo.text }}</span>
          <button 
            @click="deleteTodo(todo.id)" 
            class="btn btn-delete"
          >
            删除
          </button>
        </div>
      </div>
      
      <!-- 输入区域 -->
      <div class="input-section">
        <input 
          v-model="newTodo"
          @keypress="handleKeyPress"
          type="text" 
          placeholder="请输入待办事项..."
          class="todo-input"
        />
        <button 
          @click="addTodo" 
          class="btn btn-add"
        >
          添加
        </button>
      </div>
      
      <!-- 清空按钮 -->
      <div class="clear-section">
        <button 
          @click="clearAll" 
          class="btn btn-clear"
        >
          清空所有
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.todo-app {
  min-height: 100vh;
  background-color: #f5f5f5;
  padding: 40px 20px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.container {
  max-width: 800px;
  margin: 0 auto;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

.title {
  text-align: center;
  font-size: 32px;
  font-weight: 600;
  color: #333;
  margin: 0;
  padding: 40px 20px 30px;
  background: linear-gradient(135deg, #6c7b7f 0%, #b8c6db 100%);
  color: white;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.todo-list {
  padding: 20px;
  min-height: 200px;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 20px;
  margin-bottom: 12px;
  background: #fafafa;
  border-radius: 8px;
  border-left: 4px solid #e0e0e0;
  transition: all 0.3s ease;
}

.todo-item:hover {
  background: #f0f0f0;
  border-left-color: #667eea;
  transform: translateX(2px);
}

.todo-text {
  font-size: 16px;
  color: #333;
  flex: 1;
  margin-right: 15px;
}

.input-section {
  display: flex;
  gap: 12px;
  padding: 20px;
  background: #f9f9f9;
  border-top: 1px solid #eee;
}

.todo-input {
  flex: 1;
  padding: 12px 16px;
  border: 2px solid #e0e0e0;
  border-radius: 6px;
  font-size: 16px;
  outline: none;
  transition: all 0.3s ease;
}

.todo-input:focus {
  border-color: #667eea;
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
}

.todo-input::placeholder {
  color: #999;
}

.btn {
  padding: 12px 24px;
  border: none;
  border-radius: 6px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
  outline: none;
}

.btn:hover {
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.btn-add {
  background: #4CAF50;
  color: white;
  min-width: 80px;
}

.btn-add:hover {
  background: #45a049;
}

.btn-delete {
  background: #f44336;
  color: white;
  padding: 8px 16px;
  font-size: 12px;
}

.btn-delete:hover {
  background: #da190b;
}

.clear-section {
  padding: 20px;
  text-align: center;
  background: #f9f9f9;
  border-top: 1px solid #eee;
}

.btn-clear {
  background: #6c757d;
  color: white;
  min-width: 120px;
}

.btn-clear:hover {
  background: #5a6268;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .todo-app {
    padding: 20px 10px;
  }
  
  .title {
    font-size: 24px;
    padding: 30px 15px 20px;
  }
  
  .input-section {
    flex-direction: column;
  }
  
  .todo-item {
    flex-direction: column;
    align-items: stretch;
    gap: 10px;
  }
  
  .todo-text {
    margin-right: 0;
    margin-bottom: 8px;
  }
}
</style>
