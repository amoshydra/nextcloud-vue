<!--
 - @copyright Copyright (c) 2020 Marco Ambrosini <marcoambrosini@pm.me>
 -
 - @author Marco Ambrosini <marcoambrosini@pm.me>
 -
 - @license GNU AGPL version 3 or any later version
 -
 - This program is free software: you can redistribute it and/or modify
 - it under the terms of the GNU Affero General Public License as
 - published by the Free Software Foundation, either version 3 of the
 - License, or (at your option) any later version.
 -
 - This program is distributed in the hope that it will be useful,
 - but WITHOUT ANY WARRANTY; without even the implied warranty of
 - MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
 - GNU Affero General Public License for more details.
 -
 - You should have received a copy of the GNU Affero General Public License
 - along with this program. If not, see <http://www.gnu.org/licenses/>.
 -
 -->

<docs>

### General description

The button

### Usage

</docs>
<template>
	<button class="button"
	disabled="disabled" 
	:class="{
		'button--wide': isWide,
		'button--primary': isPrimary,
		}"
	@click="handleClick">
		<div class="button__icon" v-if="hasIcon">
			<slot />
		</div>
		<span v-if="hasText" class="">{{ text }}</span>
	</button>
</template>

<script>

export default {
	name: 'Button',

	props: {
		/**
		 * Toggle the disabled state for the button
		 */
		disabled: {
			type: Boolean,
			default: false,
		},
		/**
		 * Specify whether the button background should have primary color.
		 * Accepted values: primary, error, warning, success.
		 */
		backgroundColor: {
			type: String,
			default: '',
			validator: function(value) {
				return ['primary', 'error', 'warning', 'successs'].indexOf(value) !== -1
			}
		},

		/**
		 * Specify whether the button should span the whole width of the container
		 */
		isWide: {
			type: Boolean,
			default: false,
		},

		/**
		 * The text of the button
		 */
		text: {
			type: String,
			default: '',
		},
	},

	computed: {
		
		hasIcon() {
			return
		},

		hasText() {
			return !this.text
		},

		backgroundStyle() {
			if (this.backgroundColor) {
				return `backgroundColor: var(--color-${this.backgroundColor})`
			} else {
				return ''
			}
		}
	},

	mounted() {
		this.getIconComponent()
	},

	methods: {
		getIconComponent() {
			return () => import(`@/node_modules/vue-material-design-icons/${icon}`)
		},
	},
}

</script>

<style lang="scss" scoped>

.button {
	height: $clickable-area;
	&--primary {
		background-color: var(--color-primary);
		color: var(--color-primary-text)
	}
	&--wide {
		width: 100%;
	}
}

</style>
