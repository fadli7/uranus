<template>
  <div class="section">
		<div class="container">
				<div class="columns">
						<div class="column is-6 is-offset-3">

								<div class="box">

										<div class='is-flex is-horizontal-center'>
												<figure class="image is-128x128 has-text-centered">
														<img class="is-rounded" :src="image">
												</figure> 
										</div>

										<br>

										<div class="field">
												<label class="label">Nama Depan</label>
												<div class="control has-icons-left">
														<input v-model="firstName" class="input" type="text" placeholder="Text input">
														<span class="icon is-small is-left">
													<i class="fas fa-user"></i>
												</span>
												</div>
										</div>

										<div class="field">
												<label class="label">Nama Belakang</label>
												<div class="control has-icons-left">
														<input v-model="lastName" class="input" type="text" placeholder="Text input">
														<span class="icon is-small is-left">
													<i class="fas fa-user"></i>
												</span>
												</div>
										</div>

										<div class="field">
												<label class="label">Username</label>
												<div class="control has-icons-left">
														<input v-model="username" class="input" type="text" placeholder="Text input" >
														<span class="icon is-small is-left">
													<i class="fas fa-user-secret"></i>
												</span>
												</div>
										</div>

										<div class="field">
												<label class="label">Email</label>
												<div class="control has-icons-left">
														<input class="input" type="email" placeholder="Email input" value="hello@">
														<span class="icon is-small is-left">
													<i class="fas fa-envelope"></i>
												</span>
												</div>
										</div>

										<div class="field">
												<label class="label">Tentang Saya</label>
												<div class="control">
														<textarea class="textarea" placeholder="Textarea"></textarea>
												</div>
										</div>
										<div class="field">
												<div class="control">
														<button class="button is-primary is-fullwidth">Update Data</button>
												</div>
										</div>
								</div>

								<hr>
								<h3 class="subtitle">Ganti Password</h3>
								<div class="box">

										<div class="field">
												<label class="label">Password Baru</label>
												<div class="control has-icons-left">
														<input class="input" type="text" placeholder="Text input" value="bulma">
														<span class="icon is-small is-left">
													<i class="fas fa-key"></i>
												</span>
												</div>
										</div>

										<div class="field">
												<label class="label">Ulangi Password</label>
												<div class="control has-icons-left">
														<input class="input" type="email" placeholder="Email input" value="hello@">
														<span class="icon is-small is-left">
													<i class="fas fa-key"></i>
												</span>
												</div>
										</div>

										<div class="field">
												<div class="control">
														<button class="button is-primary is-fullwidth">Ganti Password</button>
												</div>
										</div>
								</div>
						</div>
				</div>

		</div>
</div>
</template>

<script>
export default {
	data() {
		return {
			username: null,
			firstName: null,
			lastName: null,
			image: null
		}
	},
	mounted() {
		console.log(this.$auth.user)
		this.username = this.$auth.user.username
		this.firstName = this.$auth.user.firstName
		this.lastName = this.$auth.user.lastName
		this.image = this.$auth.user.image
	},
}
</script>