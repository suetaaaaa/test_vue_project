<template>
	<div class="post_list" v-if="posts.length > 0">
		<h3>Posts list</h3>
		<PostItem
			v-for="post in posts"
			:post="post"
			:key="post.id"
			@remove="$emit('remove', post)"
		/>
	</div>
	<h2 v-else style="color: red">
		Oops... Seems like no posts there...
	</h2>
</template>

<script>
import PostItem from './PostItem.vue';

export default {
	components: {
		PostItem
	},
	props: {
		posts: {
			type: Array,
			required: true,
		}
	},
}
</script>

<style scoped>
.post_list{
	margin-top: 15px;
}
</style>