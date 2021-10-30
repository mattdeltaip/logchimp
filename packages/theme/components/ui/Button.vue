<template>
	<div
		class="button"
		:class="[
			`button-${type}`,
			loading ? 'button-loading' : '',
			disabled ? 'button-primary-disabled' : ''
		]"
		@click="click"
	>
		<slot />
		<div v-if="loading" class="button-loader">
			<loader-icon />
		</div>
	</div>
</template>

<script>
// icons
import LoaderIcon from "../icons/Loader";

export default {
	name: "Button",
	components: {
		LoaderIcon
	},
	props: {
		type: {
			type: String,
			required: true
		},
		loading: {
			type: Boolean,
			default: false
		},
		disabled: {
			type: Boolean,
			default: false
		}
	},
	methods: {
		click() {
			if (this.loading) return;
			if (this.disabled) return;
			this.$emit("click");
		}
	}
};
</script>

<style lang='sass'>
.button
	position: relative
	padding: 0.875rem 1.5rem
	border-radius: var(--border-radius-default)
	font-weight: 500
	display: flex
	justify-content: center
	cursor: pointer
	user-select: none

.button-loader
	border-radius: var(--border-radius-default)
	display: flex
	justify-content: center
	align-items: center
	width: 100%
	height: 100%
	position: absolute
	top: 0
	bottom: 0
	left: 0
	right: 0
	cursor: default

	svg
		width: 1.5rem
		height: 1.5rem
		animation-name: spinner
		animation-duration: 1.1s
		animation-direction: normal
		animation-timing-function: linear
		animation-iteration-count: infinite

.button-loading
	opacity: 0.8
	cursor: wait

@keyframes spinner
	0%
		transform: rotate(0deg)

	100%
		transform: rotate(360deg)

.button-primary
	background-color: var(--color-brand-color)
	color: var(--color-white)

	.button-loader
		background-color: var(--color-brand-color)

		svg
			stroke: var(--color-white)

.button-outline
	border: 1px solid var(--color-white-light)

	&:hover
		border-color: var(--color-white)

.button-background
	color: var(--color-brand-color)

	.button-loader
		background-color: var(--color-gray-97)

		svg
			stroke: var(--color-gray-90)

	&:hover
		background-color: var(--color-gray-97)

.button-primary-disabled
	opacity: 0.7
	cursor: not-allowed
</style>