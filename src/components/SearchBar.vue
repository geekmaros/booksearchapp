<template>
	<div>
		<div class="bar">

	<input class="input is-rounded is-5" v-model="bookname" type="text" placeholder="Search Books..📖"> 
	<a class="button is-info is-rounded" @click="searchBooks()">Search 📖 </a>	
	</div>
		
	</div>
	
</template>

<script>
export default {

  name: 'SearchBar',

  data() {
    return {
    	bookname: '',

    };
  },
  methods:{
  	searchBooks(){
  		let bookName = this.bookname
  		this.$emit('searchB', bookName);
  	}
  }
};
</script>

<style lang="css" scoped>
.bar{
	display: flex
}
</style>
