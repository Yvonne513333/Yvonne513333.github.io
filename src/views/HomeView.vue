<script>


export default {
  data() {
    return {
      article: '',
      articles: [],
      selectedTab: '',
    }
  },

  methods: {
    // 新增文章
    addArticle() {
      // 如果 input 框中有內容才執行新增
      if (this.article.trim() !== '') {
        // 將文章內容加入到 articles 陣列中
        this.articles.push(this.article);
        // 清空 input 框
        this.article = '';
      }
    },

    // 刪除指定的資料
    deleteArticle(index) {
      this.articles.splice(index, 1);
    },

    // 編輯文章內容
    editArticle(index) {
      // 提示用戶編輯文章
      const content = prompt('回覆文章', this.articles[index]);
      // 檢查用戶是否輸入了內容
      if (content !== null) {
        // 更新文章內容
        this.articles[index] = content;
      }
    },

    // 切換頁籤

  },
}



</script>

<template>
  <containerall class=" bg-rose-100 w-screen h-screen flex items-center justify-center">
    <container class=" bg-rose-200 rounded-md w-[800px] h-[600px] flex flex-col border border-black">
      <top class="p-3">
        <input type="text" placeholder="請新增文章" class="w-[500px]" v-model="article">
        <button class="submit bg-rose-300 w-[50px] h-[30px] rounded-md	ml-3" type="button" @click="addArticle()">
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

      <article v-for="(article, index) in articles" :key="index"
        class="data-show p-2  grid grid-cols-3 border-b border-black">
        <!-- 每次新增一筆文章就要有這樣的欄位出現 -->
        <span class="flex items-center"><input type="checkbox" ></span>
        <span class="flex items-center">{{ article }}</span> <!-- 這裡的"第一筆"字樣要用js變數取代 -->

        <span class="flex justify-center items-center">
          <button class="bg-rose-300 w-[50px] h-[40px] rounded-lg" type="button" @v-model="articles"
            @click="editArticle(index)">
            <i class="fa-solid fa-pen-to-square"></i>
          </button>
          <button class="bg-rose-300 w-[50px] h-[40px] rounded-lg ml-3" type="button" @v-model="articles"
            @click="deleteArticle(index)">
            <i class="fa-solid fa-trash-can"></i>
          </button>
        </span>
      </article>

    </container>
  </containerall>
</template>
