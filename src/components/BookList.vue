<template>
  <div>

    <SearchBar @searchB="bookSearch" class="search is-offset-7"></SearchBar>

    <div class="wrapper" >
    <span v-if="books.length == 0"  style="color:red; font-size: 25px;">Insert a book name to search :-) </span>
    <span v-show="error" class="is-danger"  style="color:red; font-size: 25px;">{{ error }}</span> 
    
    <div class="box" v-for="book in books" >
      <Book :book="book" :id="book.id" ></Book>
    </div>
   
  </div>
    
  </div>
  


 
</template>

<script>


import Book from "./Book.vue";
import SearchBar from "./SearchBar.vue";

export default {


  name: 'BookList',

  data() {
    return {
    	books: [],
      query:'',
      show: true,
      error: '',
     
    };
  },
  components:{
    Book,
    SearchBar,
  },
  created:function (){
    console.log(this.books.length)
  	//this.fetchBooks();
  },
  methods:{
  	// fetchBooks(){ 
  	// 	fetch(`https://www.googleapis.com/books/v1/volumes?q=${this.query}`)
  	// 	.then((res) => res.json())
  	// 	.then((data)=>{
   //      console.log(data.items)
  	// 		this.books = data.items;
  	// 	})
  			
  	// 	},

     bookSearch(value){
      if(value == ''){
        this.error = "Query can'\t be an Empty String";

      }else{
        this.query = value;

      fetch(`https://www.googleapis.com/books/v1/volumes?q=${this.query}`)
      .then((res) => res.json())
      .then((data)=>{
        console.log(data.items)
        this.books = data.items;
      })
        
        this.error = "";

      }

      
    
     }
  	},
    computed:{
      img: function(bookId){
        return `http://books.google.com/books/content?id=${this.books.id}&printsec=frontcover&img=1&zoom=1&edge=curl&source=gbs_api`
      }
    },
   
};
</script>

<style lang="css" scoped>
.wrapper{
  
  margin: 0 auto;
  height: inherit;
  display: grid;
  grid-gap: 1.5em;
  padding: 20px;
  grid-template-columns: repeat(3, 1fr);
  justify-content: center;
  
  
  
}
.box{
  margin: 30px 0px px 5px;
  background-color: #d8cdcd;
  width:250px;
  padding: 5px;
  box-shadow: 0 0 35px black;
  position: relative;
  top:20px;
  bottom: 20px;
}
img{
  width: 100%;
}
.search{
  width: 50%;
  justify-content: center;
  position: relative;
  top:20px;
  bottom: 20px;
  margin-top: 25px;

}


</style>
