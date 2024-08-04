<template>
  <div id="app">
    <table>
      <thead>
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(drink, key) in drinkData" :key="key">
          <td>
            <button class="editBtn" type="button" @click="changeText(key)">
              📝
            </button>
            {{ drink.name }}
          </td>
          <td>
            <small>{{ drink.describe }}</small>
          </td>
          <td>{{ drink.price }}</td>
          <td>
            <button @click="deStorage(key)">-</button>
            {{ drink.storage }}
            <button @click="inStorage(key)">+</button>
          </td>
        </tr>
      </tbody>
    </table>

    <div v-if="currentEditKey !== null">
      <hr />
      <h4>編輯品項名稱</h4>
      <label>請輸入名稱︰</label>
      <input type="text" v-model="editName" style="margin-right: 5px" />
      <button type="button" style="margin-right: 5px" @click="editComfirm">
        確認編輯
      </button>
      <button type="button" @click="cancelEdit">取消</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
// Level 1：將菜單轉為資料格式
const drinkData = ref([
  {
    key: 0,
    name: "珍珠奶茶",
    describe: "香濃奶茶搭配QQ珍珠",
    price: 50,
    storage: 20,
  },
  {
    key: 2,
    name: "冬瓜檸檬",
    describe: "清新冬瓜配上新鮮檸檬",
    price: 45,
    storage: 18,
  },
  {
    key: 3,
    name: "翡翠檸檬",
    describe: "綠茶與檸檬的完美結合",
    price: 55,
    storage: 34,
  },
  {
    key: 4,
    name: "四季春茶",
    describe: "香醇四季春茶，回甘無比",
    price: 45,
    storage: 10,
  },
  {
    key: 5,
    name: "阿薩姆奶茶",
    describe: "阿薩姆紅茶搭配香醇鮮奶",
    price: 50,
    storage: 25,
  },
  {
    key: 6,
    name: "檸檬冰茶",
    describe: "檸檬與冰茶的清新組合",
    price: 45,
    storage: 20,
  },
  {
    key: 7,
    name: "芒果綠茶",
    describe: "芒果與綠茶的獨特風味",
    price: 55,
    storage: 18,
  },
  {
    key: 8,
    name: "抹茶拿鐵",
    describe: "抹茶與鮮奶的絕配 ",
    price: 60,
    storage: 20,
  },
]);

// Level 2：可以重新設定菜單的庫存數量
const inStorage = (key) => {
  console.log(drinkData.value[key]);
  drinkData.value[key].storage++;
};
const deStorage = (key) => {
  if (drinkData.value[key].storage > 0) {
    drinkData.value[key].storage--;
  }
};
// Level 3（挑戰）：可以重新設定品項名稱
const currentEditKey = ref(null);
const editName = ref("");

const changeText = (key) => {
  currentEditKey.value = key;
  editName.value = drinkData.value[key].name;
};

const editComfirm = () => {
  // 以編輯後的名稱重新賦值
  drinkData.value[currentEditKey.value].name = editName.value;
  // 退出編輯模式
  currentEditKey.value = null;
  // 清空編輯表單的輸入框
  editName.value = "";
};
const cancelEdit = (key) => {
  currentEditKey.value = null;
  editName.value = "";
};
</script>

<style scoped>
.editBtn {
  padding: 0;
  border: none;
  background: transparent;
}
.editBtn:hover {
  cursor: pointer;
}
</style>
