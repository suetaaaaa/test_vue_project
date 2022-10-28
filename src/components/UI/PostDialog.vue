<template>
	<div class="dialog" v-if="show" @click="hideDialog">
		<div class="dialog__content" @click.stop>
			<slot></slot>
		</div>
	</div>
</template>



<script>
export default {
	name: 'post-dialog',
	props: {
		show: {
			type: Boolean,
			default: false
		}
	},
	methods: {
		hideDialog() {
			this.$emit('update:show', false);
		}
	}
}
</script>



<style scoped>
.dialog {
	top: 0;
	bottom: 0;
	right: 0;
	left: 0;
	background: rgba(0, 0, 0, 0.5);
	position: fixed;
	display: flex;
}

.dialog__content {
	margin: auto;
	padding: 10px 15px;
	background: white;
	border-radius: 12px;
	min-height: 50px;
	min-width: 300px;
}
</style>