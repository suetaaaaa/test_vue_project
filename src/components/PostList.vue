<template>
	<div class="post-list" v-if="posts.length > 0">
		<h3>Posts list</h3>
		<transition-group name="post-list">
			<post-item
				v-for="post in posts"
				:post="post"
				:key="post.id"
				@remove="$emit('remove', post)"
			/>
		</transition-group>
	</div>
	<div class="post-list" v-else>	
		<h2 style="color: red">
			Oops... Seems like no posts there...
		</h2>
	</div>
</template>

<script>
export default {
	name: 'post-list',
	props: {
		posts: {
			type: Array,
			required: true
		}
	},
}
</script>

<style scoped>
.post-list {
	margin-top: 15px;
}

.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all .2s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}

.post-list-move {
  transition: transform 0.2s ease;
}
</style>