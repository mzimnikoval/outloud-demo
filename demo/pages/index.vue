<template>
	<main>
		<section class="box-wrapper bg-white">
			<h1>Registration Form</h1>
			<form @submit.prevent="submit">
				<div class="row">
					<div class="col">
						<div class="form-group" :class="{ 'form-group--error': $v.name.$error, 'form-group--filled' : name }">
							<input class="form-group__input" v-model.trim="$v.name.$model"/>
							<label for="">E-mail</label>
							<span class="focus-border"></span>
						</div>
						<small class="error" v-if="!$v.name.required">Name is required</small>
					</div>
				</div>
				<div class="row">
					<div class="col">
						<div class="input-group">
							<input type="text" name="first_name" id="">
						</div>
					</div>
					<div class="col">
						<div class="input-group">
							<input type="text" name="second_name" id="">
						</div>
					</div>
				</div>
				<div class="row">
					<div class="col">
						<div class="input-group">
							<select name="" id=""></select>	
						</div>							
					</div>
					<div class="col">
						<div class="input-group">
							<select name="" id=""></select>	
						</div>		
					</div>
				</div>
				<div class="row">
					<div class="col">
						<div class="input-group">
							<input type="password" name="password" id="">
						</div>
					</div>
					<div class="col">
						<div class="input-group">
							<input type="password" name="password-repeat" id="">
						</div>
					</div>
				</div>
				<div class="row">
					<div class="col">
						<label for="">Private Profile</label>						
					</div>
				</div>
				<div class="row">
					<div class="col">
						<div class="separator"></div>
					</div>
				</div>
				<div class="row">
					<div class="col">
						<div class="flex">
							<button type="submit" class="btn">Sign up</button>
							<label class="checkbox bounce">
								<input type="checkbox">
								<span>Creating an account means you’re okay with our Privacy Policy.</span>
							</label>
						</div>
					</div>
				</div>
			</form>
		</section>
	</main>
</template>

<script>
import { required, minLength } from 'vuelidate/lib/validators'

export default {
	data() {
		return {
			email: '',
			password: '',
			name: '',
			submitStatus: null		
		}
	},
	validations: {
		name: {
			required,
			minLength: minLength(4)
		}
	},
	methods: {
		submit() {
			console.log('submit!')
			this.$v.$touch()
			if (this.$v.$invalid) {
				this.submitStatus = 'ERROR'
			} else {
				// do your submit logic here
				this.submitStatus = 'PENDING'
				setTimeout(() => {
				this.submitStatus = 'OK'
				}, 500)
			}
		}
	},
}
</script>
