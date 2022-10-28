<template>
	<div class="app">
		<h1>POSTS VUE.JS</h1>
		<add-button @click="showDialog">
			Create a post
		</add-button>
		<post-dialog v-model:show="isDialogVisible">
			<PostForm
				@create="createPost"
			/>
		</post-dialog>
		<PostList
			:posts="posts"
			@remove="removePost"
		/>
	</div>
</template>



<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";

export default {
	components: {
		PostForm, PostList
	},
	data() {
		return {
			posts: [
				{
					id: 1,
					title: 'JavaScript post',
					body: 'Post description'
				},
				{
					id: 2,
					title: 'Python post',
					body: 'Post description'
				},
				{
					id: 3,
					title: 'C++ post',
					body: 'Post description'
				},
			],
			isDialogVisible: false,
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
		}
	},
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
</style>



