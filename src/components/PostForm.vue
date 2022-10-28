<template>
	<form @submit.prevent>
		<h4>Create your post!</h4>
		<post-input
			v-model.trim="post.title"
			type="text"
			placeholder="Title"
		/>
		<post-input
			v-model.trim="post.body"
			type="text"
			placeholder="Body"
		/>
		<add-button @click="createPost">
			Add my post
		</add-button>
	</form>
</template>

<script>
export default {
	data() {
		return {
			post: {
				title: '',
				body: '',
			}
		};
	},
	methods: {
		createPost() {
			this.post.id = Date.now();
			this.$emit('create', this.post);
			this.post = {
				title: '',
				body: '',
			};
		}
	},
}
</script>

<style scoped>
form {
	display: flex;
	flex-direction: column;
}
</style>