<template>
	<div class="post">
		<div>
			<div><strong>№</strong> {{ post.id }}</div>
			<div><strong>Title:</strong> {{ post.title }}</div>
			<div><strong>Body:</strong> {{ post.body }}</div>
		</div>
		<del-button @click="$emit('remove', post)">
			Delete
		</del-button>
	</div>
</template>



<script>
export default {
	name: 'post-item',
	props: {
		post: {
			type: Object,
			required: true,
		}
	},
}
</script>



<style scoped>
.post {
	margin-top: 15px;
	padding: 15px;
	border: 2px solid teal;
	display: flex;
	align-items: center;
	justify-content: space-between;
}
</style>