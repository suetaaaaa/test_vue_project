<template>
	<button class="add-btn" type="button">
		<slot></slot>
	</button>
</template>



<script>
export default {
	name: 'add-button'
}
</script>



<style scoped>
.add-btn {
	margin-top: 15px;
	padding: 10px 15px;
	background: none;
	color: teal;
	border: 1px solid teal;
	align-self: flex-end;
} 
</style>