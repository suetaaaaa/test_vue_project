<template>
	<div class="page-wrapper">
		<div
			class="page-btn page-wrapper__page-btn"
			v-for="page in totalPages"
			:key="page"
			:class="{'current-page': pageNum === page}"
			@click="$emit('change', page)"
		>
			{{ page }}
		</div>
	</div>
</template>



<script>
export default {
	name: 'pagination-bar',
	props: {
		totalPages: {
			type: Number,
			required: true
		},
		pageNum: {
			type: Number,
			required: true
		}
	},
}
</script>



<style scoped>
.page-wrapper {
	display: flex;
	margin-top: 15px;
}
.page-btn {
	padding: 10px 15px;
	border: 1px solid gray;
	align-self: flex-end;
}
.current-page {
	padding: 10px 15px;
	border: 2px solid teal;
	align-self: flex-end;
}
</style>