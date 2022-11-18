<template>
	<div class="app">
		<h1>POSTS APP WITH VUE.JS</h1>
		<post-input
			v-model="searchPosts"
			placeholder="Search the posts by title..."
		/>
		<div class="action_buttons">
			<add-button @click="showDialog">
				Create a post
			</add-button>
			<add-button @click="fetchPosts">
				Get posts
			</add-button>
			<post-filter
				v-model="selectedSort"
				:options="sortOptions"
			/>
		</div>
		<post-dialog v-model:show="isDialogVisible">
			<post-form
				@create="createPost"
			/>
		</post-dialog>	
		<post-list
			:posts="sortedAndSearchedPosts"
			@remove="removePost"
			v-if="!isPostsLoading"
		/>
		<div class="post_list" v-else>
			<h2>Loading...</h2>
		</div>
		<div ref="observer" class="observer"></div>
		<!-- <pagination-bar
			:totalPages="totalPages"
			:pageNum="pageNum"
			@change="changePage"
		/> -->
	</div>
</template>



<script>
import axios from 'axios';

export default {
	data() {
		return {
			posts: [],
			isDialogVisible: false,
			isPostsLoading: false,
			selectedSort: '',
			searchPosts: '',
			pageNum: 1,
			postsLimit: 10,
			totalPages: 0,
			sortOptions: [
				{value: 'id', name: 'Default'},
				{value: 'title', name: 'Title'},
				{value: 'body', name: 'Body'},
			]
		}
	},
	methods: {
		createPost(post) {
			this.posts.push(post);
			this.isDialogVisible = false;
		},
		removePost(post) {
			this.posts = this.posts.filter(p => p.id !== post.id);
		},
		showDialog() {
			this.isDialogVisible = true;
		},
		async fetchPosts() {
			try {
				this.isPostsLoading = true;
				const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
					params: {
						_limit: this.postsLimit,
						_page: this.pageNum
					}
				});
				this.totalPages = Math.ceil(response.headers['x-total-count'] / this.postsLimit)
				this.posts = response.data;
			} catch (e) {
				alert(`ERROR: ${e}`);
			} finally {
				this.isPostsLoading = false;
			}
		},
		async loadMorePosts() {
			try {
				this.pageNum += 1;
				const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
					params: {
						_limit: this.postsLimit,
						_page: this.pageNum
					}
				});
				this.totalPages = Math.ceil(response.headers['x-total-count'] / this.postsLimit)
				this.posts = [...this.posts, ...response.data];
			} catch (e) {
				alert(`ERROR: ${e}`);
			}
		},
		// changePage(page) {
		// 	this.pageNum = page;
		// },
	},
	mounted() {
		this.fetchPosts();

		const options = {
			rootMargin: '0px',
			threshold: 1.0
		};
		const callback = (entries, observer) => {
			if (entries[0].isIntersecting && this.pageNum !== this.totalPages) {
				this.loadMorePosts();
				console.log(this.pageNum);
			}
		};
		const observer = new IntersectionObserver(callback, options);
		observer.observe(this.$refs.observer);
	},
	computed: {
		sortedPosts() {
			try { 
				return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])) 
			} catch(e) {
				return [...this.posts].sort((post1, post2) => post1[this.selectedSort] - post2[this.selectedSort])
			}
		},
		sortedAndSearchedPosts() {
			return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchPosts.toLowerCase()))
		}
	},
	watch: {
		// selectedSort(newValue) {
		// 	this.posts.sort((post1, post2) => {
		// 		return post1[newValue]?.localeCompare(post2[newValue]) // или post1[this.selectedSort]
		// 	})
		// },
		// pageNum() {
		// 	this.fetchPosts();
		// }		
	}
}
</script>



<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}

.app {
	padding: 20px;
}

.action_buttons {
	display: flex;
	align-items: center;
	justify-content: space-between;
}

.post_list{
	margin-top: 15px;
}

/* .observer {
	height: 50px;
	background-color: teal;
} */
</style>
