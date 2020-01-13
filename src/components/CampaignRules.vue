
<template>
	<div class="campaign">
		
		<h2>Where would you like to display your campaign?</h2>
		<div class="campaign__rules">
				<CampaignRulesItem
					v-for="rule in rules"
					:key="rule.id"
					:rule="rule"
					:isValid="isValid"
					:errors="errors.text"
					v-on:inputText="checkURL"
					@remove="removeTodo"
				/>
		</div>
		<Button v-if="isValid" @click="addRule" ><span>+</span>New Rule</Button>
		<!-- For presentation only -->
		<!-- <Button type="danger">New Rule</Button> -->
	</div>
</template>

<script>
	import Button from './Common/Button.vue'
	import CampaignRulesItem from './CampaignRulesItem.vue'

	let nextTodoId = 1

	export default {
		components: { 
			Button,
			CampaignRulesItem
		},
		data () {
			return {
				rules: [],
				errors: {
					type: String,
					text: 'URL is Missing'
				},
				isValid: {
					type: Boolean,
					default: true
				}
			}
		},
		methods: {
			addRule () {
				this.rules.push({
					id: nextTodoId++
				})
				return this.isValid = false;

			},
			removeTodo (idToRemove) {
				this.rules = this.rules.filter(rule => {
					return rule.id !== idToRemove
				})
				if(!this.rules.lenght) {
					return this.isValid = true;
				} 
			},
			checkURL: function (val){
				let valid = val.toString();
				
				if(!valid) {
					return (
						this.isValid = false,
						this.errors.text = 'URL is Missing'
					)		
				} else if (!this.validURL(valid)) {
					return (
						this.isValid = false,
						this.errors.text = 'Please input correct site URL'
					)
				} else {
					return (
						this.isValid = true
					)
				}
			},
            validURL: function (siteURL) {
                const re = /\b[-a-zA-Z0-9@:/=]{2,256}\.[a-z]{2,4}\b([-a-zA-Z0-9@:%_+.~#?&/=]*)?/ig;
                return re.test(siteURL);
            }
		}
	}
</script>

<style lang="scss" scoped>
	@import '../styles/common/index.scss';

	.campaign {
		padding: 1rem;
		border-top: 1px solid $c-border-l;
		h2 {
			margin-bottom: 1.5rem;
		}
		&__rules {
			display: flex;
			flex-direction: column;
			flex-wrap: wrap;
		}
	}

</style>