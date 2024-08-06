<script setup>
import { ref } from 'vue'
const data = [
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 15
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 30
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 20
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20
  }
]

const drinks = ref(data)

const editingItem = ref({})

const changeStock = (drink, amount) => {
  if (drink.stock === 0 && amount === -1) {
    return
  } else {
    drink.stock += amount
  }
}

const changeName = (drink) => {
  console.log(drink)
  editingItem.value = { ...drink }
}

const confirm = (drink) => {
  drink.name = editingItem.value.name
  editingItem.value = {}
}

const cancel = () => {
  editingItem.value = {}
}
</script>

<template>
  <table class="styled-table">
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
        <th scope="col">EDIT</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="drink in drinks" :key="drink.id">
        <td>{{ drink.name }}</td>
        <td>
          <small>{{ drink.description }}</small>
        </td>
        <td>{{ drink.price }}</td>
        <td>
          <button @click="changeStock(drink, -1)">-</button>{{ drink.stock }}
          <button @click="changeStock(drink, 1)">+</button>
        </td>
        <td>
          <button @click="changeName(drink)">修改品項</button>
          <span v-if="drink.id === editingItem.id">
            <input type="text" v-model="editingItem.name" />
            <button @click="confirm(drink)">確定</button>
            <button @click="cancel(drink)">取消</button>
          </span>
        </td>
      </tr>
    </tbody>
  </table>
</template>
<style scoped>
.styled-table {
  width: 100%;
  border-collapse: collapse;
  margin: 25px 0;
  font-size: 18px;
  text-align: left;
  background-color: #f3f3f3;
  color: #333;
}

.styled-table th,
.styled-table td {
  padding: 12px 15px;
}

.styled-table thead tr {
  background-color: #009879;
  color: #ffffff;
  text-align: left;
}

.styled-table tbody tr {
  border-bottom: 1px solid #dddddd;
}

.styled-table tbody tr:nth-of-type(even) {
  background-color: #f3f3f3;
}

.styled-table tbody tr:last-of-type {
  border-bottom: 2px solid #009879;
}

.styled-table button {
  background-color: #009879;
  border: none;
  color: white;
  padding: 5px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

.styled-table button:hover {
  background-color: #007f66;
}

.styled-table input[type='text'] {
  padding: 5px;
  font-size: 16px;
  margin: 5px 0;
}
</style>
