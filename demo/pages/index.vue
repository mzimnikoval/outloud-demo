<template>
	<main>
		<section class="box-wrapper bg-white">
			<div v-if="!submitStatus" class="form-wrapper">
				<h1>Registration Form</h1>
				<form @submit.prevent="submit">
					<div class="row">
						<div class="col">
							<div class="form-group" :class="{ 'form-group--error': $v.email.$error, 'form-group--filled' : email }">
								<input type="email" class="form-group__input" v-model.trim="$v.email.$model"/>
								<label for="">E-mail</label>
								<span class="focus-border"></span>
							</div>
							<small class="error" v-if="!$v.email.required">E-mail is required</small>
							<small class="error" v-if="!$v.email.email">E-mail has wrong format</small>
						</div>
					</div>
					<div class="row">
						<div class="col">
							<div class="form-group" :class="{ 'form-group--error': $v.firstName.$error, 'form-group--filled' : firstName }">
								<input type="text" class="form-group__input" v-model.trim="$v.firstName.$model"/>
								<label for="">First Name</label>
								<span class="focus-border"></span>
							</div>
							<small class="error" v-if="!$v.firstName.required">First name is required</small>
						</div>
						<div class="col">
							<div class="form-group" :class="{ 'form-group--error': $v.secondName.$error, 'form-group--filled' : secondName }">
								<input type="text" class="form-group__input" v-model.trim="$v.secondName.$model"/>
								<label for="">Second Name</label>
								<span class="focus-border"></span>
							</div>
							<small class="error" v-if="!$v.secondName.required">Second name is required</small>
						</div>
					</div>
					<div class="row">
						<div class="col">
							<popper
								trigger="clickToOpen" :force-show="showLang"
								:class="[showLang ? 'popover-opened' : '' ]"
								class="relative"
								:options="{
									placement: 'bottom',
								}">
								<div class="popper">
									<div class="popper__wrapper">
										<span class="popper__item" @click="language = item.name, selectLanguage = item.name, showLang = !showLang" v-for="item in languages">
											<img :src="item.flag" />
											{{item.name}}
										</span>
									</div>
								</div>

								<div class="form-select" :class="{ 'form-select--filled' : language }" slot="reference" @click="showLang = true">
									<input type="text" class="form-group__input hidden" v-model="language" autocomplete="chrome-off"/>
									<span class="form-group__input">{{selectLanguage}}</span>
									<svg width="12" height="7" viewBox="0 0 12 7" fill="none" xmlns="http://www.w3.org/2000/svg">
										<path d="M6.71985 6.78C6.57934 6.92069 6.3887 6.99982 6.18985 7L5.80985 7C5.61144 6.9977 5.42157 6.91888 5.27985 6.78L0.149852 1.64C0.102988 1.59352 0.0657908 1.53822 0.0404065 1.47729C0.0150221 1.41636 0.00195288 1.35101 0.00195288 1.285C0.00195287 1.21899 0.0150221 1.15364 0.0404064 1.09271C0.0657908 1.03178 0.102988 0.976482 0.149852 0.93L0.859852 0.22C0.905475 0.173437 0.959931 0.136444 1.02003 0.11119C1.08013 0.085936 1.14466 0.0729284 1.20985 0.0729284C1.27504 0.0729284 1.33958 0.085936 1.39967 0.11119C1.45977 0.136444 1.51423 0.173437 1.55985 0.22L5.99985 4.67L10.4399 0.22C10.4863 0.173136 10.5416 0.135939 10.6026 0.110554C10.6635 0.0851698 10.7288 0.0721002 10.7949 0.0721002C10.8609 0.0721002 10.9262 0.0851698 10.9871 0.110554C11.0481 0.135939 11.1034 0.173136 11.1499 0.22L11.8499 0.93C11.8967 0.976481 11.9339 1.03178 11.9593 1.09271C11.9847 1.15364 11.9978 1.21899 11.9978 1.285C11.9978 1.35101 11.9847 1.41636 11.9593 1.47729C11.9339 1.53822 11.8967 1.59352 11.8499 1.64L6.71985 6.78Z" fill="#C0CCDA"/>
									</svg>
								</div>
							</popper>					
						</div>
						<div class="col">						
							<popper
								trigger="clickToOpen" :force-show="show"
								:class="[show ? 'popover-opened' : '' ]"
								class="relative"
								:options="{
									placement: 'bottom',
								}">
								<div class="popper">
									<div class="popper__wrapper">
										<span class="popper__item" @click="country = item.name.common, selectCountry = item.name.common, show = !show" v-for="item in countries">
											{{item.name.common}}
										</span>
									</div>
								</div>

								<div class="form-select" :class="{ 'form-select--filled' : country }" slot="reference" @click="open">
									<input type="text" class="form-group__input hidden" v-model="country" autocomplete="chrome-off"/>
									<span class="form-group__input">{{selectCountry}}</span>
									<svg width="12" height="7" viewBox="0 0 12 7" fill="none" xmlns="http://www.w3.org/2000/svg">
										<path d="M6.71985 6.78C6.57934 6.92069 6.3887 6.99982 6.18985 7L5.80985 7C5.61144 6.9977 5.42157 6.91888 5.27985 6.78L0.149852 1.64C0.102988 1.59352 0.0657908 1.53822 0.0404065 1.47729C0.0150221 1.41636 0.00195288 1.35101 0.00195288 1.285C0.00195287 1.21899 0.0150221 1.15364 0.0404064 1.09271C0.0657908 1.03178 0.102988 0.976482 0.149852 0.93L0.859852 0.22C0.905475 0.173437 0.959931 0.136444 1.02003 0.11119C1.08013 0.085936 1.14466 0.0729284 1.20985 0.0729284C1.27504 0.0729284 1.33958 0.085936 1.39967 0.11119C1.45977 0.136444 1.51423 0.173437 1.55985 0.22L5.99985 4.67L10.4399 0.22C10.4863 0.173136 10.5416 0.135939 10.6026 0.110554C10.6635 0.0851698 10.7288 0.0721002 10.7949 0.0721002C10.8609 0.0721002 10.9262 0.0851698 10.9871 0.110554C11.0481 0.135939 11.1034 0.173136 11.1499 0.22L11.8499 0.93C11.8967 0.976481 11.9339 1.03178 11.9593 1.09271C11.9847 1.15364 11.9978 1.21899 11.9978 1.285C11.9978 1.35101 11.9847 1.41636 11.9593 1.47729C11.9339 1.53822 11.8967 1.59352 11.8499 1.64L6.71985 6.78Z" fill="#C0CCDA"/>
									</svg>
								</div>
							</popper>
						</div>
					</div>
					<div class="row">
						<div class="col">
							<div class="form-group" :class="{ 'form-group--error': $v.password.$error, 'form-group--filled' : password }">
								<input :type="[showPassword ? 'text' : 'password']" class="form-group__input" v-model.trim="$v.password.$model"/>
								<label for="">Password</label>
								<svg width="24" height="20" viewBox="0 0 24 20" fill="none" xmlns="http://www.w3.org/2000/svg" :class="{ 'active' : showPassword }" @click="showPassword = !showPassword">
									<path fill-rule="evenodd" clip-rule="evenodd" d="M12 19C16.563 19 20.063 16 22.5 10C20.063 4 16.563 1 12 1C7.437 1 3.937 4 1.5 10C3.937 16 7.437 19 12 19ZM12 14.5C10.8076 14.4966 9.66498 14.0214 8.82181 13.1782C7.97864 12.335 7.50343 11.1924 7.5 10C7.5 7.525 9.525 5.5 12 5.5C14.475 5.5 16.5 7.525 16.5 10C16.5 12.475 14.475 14.5 12 14.5Z" stroke="#C0CCDA" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
								</svg>
								<span class="focus-border"></span>
							</div>
							<small class="error" v-if="!$v.password.required">Password is required</small>
							<small class="error" v-if="!$v.password.minLength">Password must be at least 8 characters long</small>
						</div>
						<div class="col">
							<div class="form-group" :class="{ 'form-group--error': $v.confirmPassword.$error, 'form-group--filled' : confirmPassword }">
								<input :type="[showPasswordRepeat ? 'text' : 'password']" class="form-group__input" v-model.trim="$v.confirmPassword.$model"/>
								<label for="">Confirm Password</label>
								<svg width="24" height="20" viewBox="0 0 24 20" fill="none" xmlns="http://www.w3.org/2000/svg" :class="{ 'active' : showPasswordRepeat }" @click="showPasswordRepeat = !showPasswordRepeat">
									<path fill-rule="evenodd" clip-rule="evenodd" d="M12 19C16.563 19 20.063 16 22.5 10C20.063 4 16.563 1 12 1C7.437 1 3.937 4 1.5 10C3.937 16 7.437 19 12 19ZM12 14.5C10.8076 14.4966 9.66498 14.0214 8.82181 13.1782C7.97864 12.335 7.50343 11.1924 7.5 10C7.5 7.525 9.525 5.5 12 5.5C14.475 5.5 16.5 7.525 16.5 10C16.5 12.475 14.475 14.5 12 14.5Z" stroke="#C0CCDA" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
								</svg>
								<span class="focus-border"></span>
							</div>
							<small class="error" v-if="!$v.confirmPassword.required">Confirm password is required</small>
							<small class="error" v-if="!$v.confirmPassword.sameAsPassword">The password confirmation does not match</small>
						</div>
					</div>
					<div class="row">
						<div class="col">
							<div class="d-flex justify-space-between align-items-center flex-xs-row">
								<label for="">Private Profile</label>	
								<div class="h-60">
									<div class="toggle-button-cover">
										<div class="button-cover">
											<div class="button b2" id="button-13">
											<input type="checkbox" class="checkbox">
											<div class="knobs">
												<span></span>
											</div>
											<div class="layer"></div>
											</div>
										</div>
									</div>							
								</div>					
							</div>
						</div>
					</div>
					<div class="row">
						<div class="col">
							<div class="separator"></div>
						</div>
					</div>
					<div class="row">
						<div class="col">
							<div class="d-flex justify-space-between flex-xs-reverse">
								<button type="submit" class="btn">Sign up</button>
								<label class="checkboxx bounce">
									<div class="relative">
										<input type="checkbox" v-model.trim="$v.privacyPolicy.$model">
										<svg viewBox="0 0 21 21">
											<polyline points="5 10.75 8.5 14.25 16 6"></polyline>
										</svg>
									</div>
									<span>Creating an account means you’re okay with our Privacy Policy.</span>
								</label>
							</div>
						</div>
					</div>
				</form>			
			</div>	
			<transition name="fade">
				<div v-if="submitStatus" class="form-success">
					<div class="success-badge">
						<svg width="31" height="21" viewBox="0 0 31 21" fill="none" xmlns="http://www.w3.org/2000/svg">
							<path d="M2 9.84615L11.35 19L28.7143 2" stroke="white" stroke-width="4" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
						</svg>
					</div>
					<h1 class="lower-margin">Success registration</h1>
					<p class="text-18 text-center">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris lobortis gravida ex, at maximus lorem condimentum ut. Cras purus mauris, convallis vitae sollicitudin sed, fringilla lobortis lorem. </p>
				</div>	
			</transition>
		</section>
	</main>
</template>

<script>
import { required, email, sameAs, minLength } from 'vuelidate/lib/validators'
import Popper from 'vue-popperjs';
import 'vue-popperjs/dist/vue-popper.css';

import Eye from "~/components/svg/eye";

export default {
	components: { Popper, Eye },
	data() {
		return {
			email: '',
			firstName: '',
			secondName: '',
			language: '',
			country: '',
			password: '',
			confirmPassword: '',
			privateProfile: false,
			privacyPolicy: false,
			submitStatus: false,
			countries: [],
			languages: [
				{ name: 'Slovak', flag: 'slovak_flag.svg'},
				{ name: 'English', flag: 'unitedkingdom_flag.svg'},				
			],
			showPassword: false,
			showPasswordRepeat: false,
			selectCountry: 'Country',
			selectLanguage: 'Language',
			showCountryPopover: false,
			show: false,
			showLang: false
		}
	},
	validations: {
		email: {
			required,email
		},
		firstName: {
			required
		},
		secondName: {
			required
		},
		password: {
			required,
			minLength: minLength(8)
		},
		confirmPassword: {
			required,
			sameAsPassword: sameAs('password')
		},
		privacyPolicy : { sameAs: sameAs( () => true ) }
	},
	mounted() {
		this.getCountries()
	},
	methods: {
		submit() {
			console.log('submit!')
			this.$v.$touch()
			if (this.$v.$invalid) {
				this.submitStatus = false
			} else {
				// do your submit logic here
				this.submitStatus = true
			}
		},
		async getCountries() {
			const countries = await this.$axios.$get('https://restcountries.com/v3.1/all')
			this.countries = countries
		},
		open(){
	    	this.show= true;
        },
        close() {
            this.show = false;
        }
	},
}
</script>
