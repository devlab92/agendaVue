<template>
	<div id="modal">
		<div id="modalBox">
			<div id="modalHeader">
				<p>{{ contact ? 'Editar' : 'Criar novo'}} contato</p>
			</div>
			<hr />
			<div id="modalBody">
				<div>
					<p>Nome</p>
					<input type="text" v-model="name" />
				</div>
				<div>
					<p>E-mail</p>
					<input type="text" v-model="email" />
				</div>
				<div>
					<p>Telefone</p>
					<input type="text" v-model="phone" v-mask="'(##) #####-####'" />
				</div>
			</div>
			<hr />
			<div id="modalFooter">
				<div id="cancel" @click="close()">
					<p>Cancelar</p>
				</div>
				<div id="save">
					<div id="saveBtn" :class="'saveDisabled'" @click="save()">
						<p>Salvar</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'ContactForm',
	props: ['contact'],
	data() {
		return {
			name: '',
			email: '',
			phone: '',
			thisContact: {}
		}
	},
	watch: {
		name() {
			this.activeSaveBtn(this.name)
		},
		email() {
			this.activeSaveBtn(this.email)
		},
		phone() {
			this.activeSaveBtn(this.phone)
		},
	},
	mounted() {
		if (this.contact) {
			this.name = this.contact.name
			this.email = this.contact.email
			this.phone = this.contact.phone
		}
	},
	methods: {


		save() {
			var removeClass = function (contact, contactsList) {
				setTimeout(() => {
					let element = document.getElementById('id_' + contact.id)
					if (element) {
						element.classList.remove('selected')
						delete contactsList.find(ctt => ctt.id == contact.id).selected
					}
				}, 10000)
			}

			if (!this.contact) {
				this.thisContact = {
					id: (performance.now().toString(36) + Math.random().toString(36)).replace(/\./g, ""),
					name: this.name,
					email: this.email,
					phone: this.phone,
					selected: 'selected',
					removeClassFn: removeClass
				}
			} else {
				this.thisContact = {
					name: this.name,
					email: this.email,
					phone: this.phone,
					id: this.contact.id
				}
			}


			this.name = ''
			this.email = ''
			this.phone = ''
			this.$emit('addOrEditContact', this.thisContact)
			this.close()
		},
		activeSaveBtn(el) {
			let thisEl = el.trim()

			let element = document.getElementById('saveBtn')
			if (thisEl.length > 0) {
				element.classList.remove('saveDisabled')
			} else {
				element.classList.add('saveDisabled')
			}
		},
		close() {
			this.$emit('close', false)
		}
	}

}
</script>

<style scoped>
#modal {
	width: 100%;
	height: 100%;
	background-color: rgba(0, 0, 0, 0.4);
	z-index: 1;
	position: fixed;
	top: 0;
	left: 0;
	display: flex;
	justify-content: center;
	color: var(--dark);
}

#modalBox {
	position: absolute;
	width: 95%;
	max-width: 27rem;
	margin: 15vh 0.5rem 0 0.5rem;
	padding: 0 0 0.5rem 0;
	border-radius: 16px;
	box-shadow: 0 16px 10px 0 rgba(0, 0, 0, 0.16);
	background-color: var(--white-two);
}

#modalBox hr {
	display: block;
	border: 0;
	border-top: 1px solid #c0c3d2;
	margin: 0;
	padding: 0;
}

#modalHeader {
	padding: 1rem;
}
#modalBody {
	padding: 1rem;
	font-size: 0.875rem;
}

#modalBody div {
	margin: 10px;
}

#modalBody p {
	margin: 0 0 0.25em 0;
}

#modalBody input {
	width: -webkit-fill-available;
	height: 2rem;
	border-radius: 4px;
	border: solid 1px #c0c3d2;
	padding: 0 0 0 0.625rem;
}

#modalBody input:focus {
	box-shadow: 0 0 0 0;
	outline: 0;
}

#modalBody > div:last-child {
	max-width: 8rem;
}

#modalFooter {
	height: 3.938rem;
	display: flex;
	flex-direction: row;
	align-items: center;
	margin: 0 1rem;
	position: relative;
	float: right;
}

#cancel {
	margin-right: 1rem;
}
#cancel p {
	cursor: pointer;
	color: #fa7268;
	font-weight: 500;
}

#save div {
	display: flex;
	justify-content: center;
	align-items: center;
	cursor: pointer;
	width: 4.5rem;
	height: 2rem;
	border-radius: 16px;
	box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.16),
		0 0 0 0.5px var(--black-8), inset 0 0 0 0.5px var(--black-8),
		0 2px 4px 0.5px rgba(0, 0, 0, 0.16);
	font-size: 0.875rem;
	font-weight: 500;
	font-stretch: normal;
	font-style: normal;
	line-height: normal;
	letter-spacing: normal;
	text-align: center;
	color: var(--white-two);
	background-color: #fa7268;
}

.saveDisabled {
	opacity: 0.32;
}

@media (max-width: 479px) {
	#modalFooter {
		width: 100%;
		margin: 0;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		gap: .25rem;
	}
	#modalFooter > div:first-child{
		margin: 0;
	}
}
</style>
