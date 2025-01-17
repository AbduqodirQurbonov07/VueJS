<template>
  <div
    class="w-screen h-screen flex flex-col justify-center gap-8 items-center bg-slate-950"
  >
    <div class="flex gap-2">
      <input
        v-model="todotitle"
        class="text-slate-50 p-2 w-[300px] rounded border border-[#ED4B96] bg-slate-950"
        type="text"
        placeholder=" Add Todo List  "
      />
      <button
        @click="submittodo"
        class="border px-2 py-2 text-stone-50 bg-green-700 rounded border-[#ED4B96] hover:bg-[#FF6A87] transition delay-300"
      >
        Qo'shish
      </button>
    </div>
    <div class="flex flex-col gap-4">
      <div
        v-if="todos.length == 0"
        class="p-4 mb-4 text-lg rounded-lg bg-slate-800 text-red-400"
        role="alert"
      >
        <span>Bajarilgan mashqlar mavjud emas...</span>
      </div>
      <div v-else class="flex flex-col gap-4">
        <p class="text-red-500 font-semibold text-lg">
          Bajarilmagan mashqlar : {{ uncompletedTodos.length }}
        </p>
        <li
          v-for="(todo, index) in uncompletedTodos"
          :key="todo.id"
          class="w-[320px] flex justify-between items-center text-slate-50 bg-slate-800 rounded-lg p-3"
        >
          <p>
            <span>{{ index + 1 }}. </span>
            <span>{{ todo.title }}</span>
          </p>
          <p class="flex gap-1">
            <button
              :id="todo.id"
              @click="deleteTodos"
              class="flex w-8 h-8 justify-center items-center border border-slate-500 bg-slate-800 rounded"
            >
              <img
                class="animate-pulse h-3 w-3"
                src="../images/delete.svg"
                alt=""
              />
            </button>

            <button
              :id="todo.id"
              @click="CompletedTodos"
              class="flex w-8 h-8 justify-center items-center border border-slate-500 bg-slate-800 rounded"
            >
              <img
                class="animate-pulse w-3 h-3"
                src="../images/complete.svg"
                alt=""
              />
            </button>
          </p>
        </li>
      </div>
      <div class="flex flex-col gap-2">
        <p class="text-green-500 font-semibold text-lg">
          Bajarilgan mashqlar : {{ completedTodos.length }}
        </p>
        <li
          v-for="(todo, index) in completedTodos"
          :key="todo.id"
          class="w-[320px] flex justify-between items-center text-slate-50 bg-slate-800 rounded-lg p-3"
        >
          <p>
            <span>{{ index + 1 }}. </span>
            <span>{{ todo.title }}</span>
          </p>
          <p class="flex gap-1">
            <button
              @click="deleteTodos"
              :id="todo.id"
              class="flex w-8 h-8 justify-center items-center border border-slate-500 bg-slate-800 rounded"
            >
              <img
                class="animate-pulse h-3 w-3"
                src="../images/delete.svg"
                alt=""
              />
            </button>
            <button
              :id="todo.id"
              @click="unCompletedTodos"
              class="flex w-8 h-8 justify-center items-center border border-slate-500 bg-slate-800 rounded"
            >
              <img
                class="animate-pulse w-3 h-3"
                src="../images/arrow.svg"
                alt=""
              />
            </button>
          </p>
        </li>
      </div>
    </div>
  </div>
</template>
<script setup>
import { computed, reactive, ref } from "vue";
let todos = ref([]);
let completedTodos = ref([]);
let uncompletedTodos = ref([]);
let todotitle = ref("");
function getData() {
  fetch("http://localhost:3000/todos")
    .then((response) => response.json())
    .then((data) => {
      todos.value = data;
      // console.log(todos.value);
      completedTodos = todos.value.filter((e) => {
        return e.completed === true;
      });
      uncompletedTodos = todos.value.filter((e) => {
        return e.completed === false;
      });
      // console.log(uncompletedTodos);
    });
}
getData();
async function submittodo() {
  const url = "http://localhost:3000/todos";
  let data = {
    title: todotitle.value,
    completed: false,
  };

  try {
    const response = await fetch(url, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(data),
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const result = await response.json();
    document.location.reload();
  } catch (error) {
    console.error("Error sending POST request:", error);
  }
}
async function CompletedTodos(e) {
  if (e.target.nodeName == "BUTTON") {
    const url = `http://localhost:3000/todos/${e.target.id}`;
    let data = {};
    console.log(url);

    try {
      const getresponse = await fetch(url);
      const getdata = await getresponse.json();
      data = { title: getdata.title, completed: true };
      const respone = await fetch(url, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
      });
      if (!respone.ok) {
        throw new Error(`HTTP error! status:${respone.status}`);
      }
      const result = await respone.json();
      console.log("PUT ", result);

      window.location.reload();
    } catch (error) {
      // console.error("Error sending PUT request:", error);
    }
  }
}

async function unCompletedTodos(e) {
  if (e.target.nodeName == "BUTTON") {
    const url = `http://localhost:3000/todos/${e.target.id}`;
    let data = {};
    console.log(url);

    try {
      const getresponse = await fetch(url);
      const getdata = await getresponse.json();
      data = { title: getdata.title, completed: false };
      const respone = await fetch(url, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
      });
      if (!respone.ok) {
        throw new Error(`HTTP error! status:${respone.status}`);
      }
      const result = await respone.json();
      console.log("PUT ", result);

      window.location.reload();
    } catch (error) {
      // console.error("Error sending PUT request:", error);
    }
  }
}
async function deleteTodos(e) {
  if (e.target.nodeName == "BUTTON") {
    const url = `http://localhost:3000/todos/${e.target.id}`;
    let data = {};
    console.log(url);

    try {
      const getresponse = await fetch(url);
      const getdata = await getresponse.json();
      data = { title: getdata.title, completed: false };
      const respone = await fetch(url, {
        method: "DELETE",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
      });
      if (!respone.ok) {
        throw new Error(`HTTP error! status:${respone.status}`);
      }
      const result = await respone.json();
      console.log("PUT ", result);

      window.location.reload();
    } catch (error) {
      // console.error("Error sending PUT request:", error);
    }
  }
}
</script>
<style></style>
