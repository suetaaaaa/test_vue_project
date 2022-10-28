<template>
	<button class="del-btn" type="button">
		<slot></slot>
	</button>
</template>



<script>
export default {
	name: 'del-button'
}
</script>



<style scoped>
.del-btn {
	padding: 10px 15px;
	background: none;
	color: red;
	border: 1px solid red;
	align-self: flex-end;
}
</style>