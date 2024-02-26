<script setup>
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <containerall class=" bg-rose-100 w-screen h-screen flex items-center justify-center">
    <container class=" bg-rose-200 rounded-md w-[800px] h-[600px] flex flex-col border border-black">
      <top class="p-3">
        <input type="text" name="" id="" placeholder="請新增文章" class="w-[500px]">
        <button class="submit bg-rose-300 w-[50px] h-[30px] rounded-md	ml-3" type="button">
          <i class="fa-regular fa-file"></i>        
        </button>
      </top>
      
      <middle class="mt-2 border-b border-[#333]">
        <button class="bg-orange-300 p-3 ml-3 focus:bg-orange-200 border-black rounded-md" type="button">全部</button>
        <button class="bg-orange-300 p-3 ml-3 focus:bg-orange-200 border-black rounded-md" type="button">已執行</button>
        <button class="bg-orange-300 p-3 ml-3 focus:bg-orange-200 border-black rounded-md" type="button">未執行</button>
      </middle>

      <div class="todo p-2 border-b border-black  grid grid-cols-3">
            <span>執行</span>
            <span>事項</span>
            <span class="text-center">功能</span>
      </div>

      <article class="data-show p-2  grid grid-cols-3 border-b border-black">
        <!-- 每次新增一筆文章就要有這樣的欄位出現 -->
        <span class="flex items-center"><input type="checkbox" name="" id=""></span>
        <span class="flex items-center">第一筆</span>  <!-- 這裡的"第一筆"字樣要用js變數取代 -->
        
        <span  class="flex justify-center items-center">
          <button class="bg-rose-300 w-[50px] h-[40px] rounded-lg" type="button">
            <i class="fa-solid fa-pen-to-square"></i>
          </button>
          <button class="bg-rose-300 w-[50px] h-[40px] rounded-lg ml-3" type="button">
            <i class="fa-solid fa-trash-can"></i>
          </button>
        </span>
      </article>

    </container>
  </containerall>
</template>
