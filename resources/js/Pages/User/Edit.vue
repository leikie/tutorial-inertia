<template>
	<Layout v-bind:title="title">
		<h1>Update Profile</h1>
		<form @submit.prevent="update">
			<div class="form-group">
				<label>Name</label>
				<input type="text" v-model="form.name">
				<p v-if="errors.name" class="error">{{ errors.name }}</p>
			</div>

			<div class="form-group">
				<label>Email</label>
				<input type="text" v-model="form.email">
				<p v-if="errors.email" class="error">{{ errors.email }}</p>
			</div>

			<button type="submit">Update</button>
		</form>
	</Layout>
</template>

<script>
	import Layout from '../../Shared/Layout.vue'

	export default {
		components: {
			Layout
		},
		data() {
			return {
				form: {
					name: this.user.name,
					email: this.user.email
				}
			}
		},
		props: {
			title: String,
			errors: Object,
			user: Object
		},
		methods: {
			update() {
				this.$inertia.put('/users/' +this.user.id, this.form)
			}
		}
	}	
</script>

<style>
	.form-group {
		margin-bottom: 5px
	}

	.error {
		color: red
	}
</style>