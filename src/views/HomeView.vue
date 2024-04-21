<script>
export default {
  data() {
    return {
      article: '',
      articleArr: [],
      switchBtn:'all',
    }
  },

  mounted() {
    // console.log(1234);  測試是否在網頁一打開即有跑函式
    if (localStorage.getItem('article')) {
      this.articleArr = JSON.parse(localStorage.getItem('article'));
    }
  },

  // 預處理妳拿到的資料，他有暫存的功能，所以我們可以拿整包資料，利用判斷式去把我們的資料做篩選
  computed:{
      selectMsg(){
        return  this.articleArr.filter((item)=>{
          if(this.switchBtn === 'all'){
            return this.articleArr;
          }else if(this.switchBtn === '已完成') {
           return item.checkBox == true;
          }else if(this.switchBtn === '未完成'){
            return item.checkBox == false;
          }
        });

      }
    },

  methods: {
    // 新增文章
    addArticle() {
      // 如果 input 框中有內容才執行新增
      if (this.article.trim() !== '') {
        // 將文章內容加入到 articleArr 陣列中
        const id = this.articleArr.length ?? 0;
        this.articleArr.push({
          id:id+1,
          msg: this.article,
          checkBox: false,
        });
        // 清空 input 框
        this.article = '';
      }
      localStorage.setItem('article', JSON.stringify(this.articleArr));
      // console.log(this.articleArr);
    },

    // 刪除指定的資料
    deleteArticle(index) {
      // console.log(index);
      this.articleArr.splice(index, 1);
      localStorage.setItem('article', JSON.stringify(this.articleArr));
    },

    // 編輯文章內容
    editArticle(index) {
      // 提示用戶編輯文章
      const content = prompt('回覆文章');
      // 檢查用戶是否輸入了內容
      if (content !== null) {
        // 更新文章內容
        this.articleArr[index].msg = content;
      }
      localStorage.setItem('article', JSON.stringify(this.articleArr));
    },

  },
}



</script>

<template>
  <containerall class=" bg-rose-100 w-screen h-screen flex items-center justify-center">
    <container class=" bg-rose-200 rounded-md w-[800px] h-[600px] flex flex-col border border-black">
      <top class="p-3">
        <input type="text" placeholder="請新增文章" class="w-[500px]" v-model="article">
        <button class="submit bg-rose-300 w-[50px] h-[30px] rounded-md ml-3" type="button" @click="addArticle()">
          <i class="fa-regular fa-file"></i>
        </button>
      </top>

      <middle class="mt-2 border-b border-[#333]">
        <button class="tab bg-orange-300 p-3 ml-3 border-black rounded-md" :class="{ 'active' : switchBtn == 'all'}" type="button" @click="switchBtn ='all'" >全部</button>

        <button class="tab bg-orange-300 p-3 ml-3 border-black rounded-md" :class="{ 'active' : switchBtn == '已完成'}" type="button" @click="switchBtn ='已完成'" >已執行</button>

        <button class="tab bg-orange-300 p-3 ml-3  border-black rounded-md" :class="{ 'active' : switchBtn == '未完成'}" type="button" @click="switchBtn ='未完成'">未執行</button>
      </middle>

      <div class="todo p-2 border-b border-black  grid grid-cols-3">
        <span>執行</span>
        <span>事項</span>
        <span class="text-center">功能</span>
      </div>

      <article v-for="(article, index) in selectMsg" :key="index"
        class="data-show p-2  grid grid-cols-3 border-b border-black">
        <!-- 每次新增一筆文章就要有這樣的欄位出現 -->
        <span class="flex items-center">
          <input type="checkbox" v-model="article.checkBox">
        </span>
        <span class="flex items-center">{{ article.msg }}</span> <!-- 這裡的"第一筆"字樣要用js變數取代 -->

        <span class="flex justify-center items-center">
          <button class="bg-rose-300 w-[50px] h-[40px] rounded-lg" type="button" @click="editArticle(index)">
            <i class="fa-solid fa-pen-to-square"></i>
          </button>
          <button class="bg-rose-300 w-[50px] h-[40px] rounded-lg ml-3" type="button" @click="deleteArticle(index)">
            <i class="fa-solid fa-trash-can"></i>
          </button>
        </span>
      </article>

    </container>
  </containerall>
</template>
<style>
.active {
  @apply bg-[#f1e394] text-black;
}
</style>
