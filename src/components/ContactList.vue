<template>
	<div id="contactList">
		<header id="listNavBar">
			<div id="firstRowNavBar">
				<div id="contactHeader">
					<p>Contatos</p>
				</div>
				<div id="emailHeader">
					<p>E-mail</p>
				</div>
			</div>
			<div id="secondRowNavBar">
				<div id="phoneHeader">
					<p>Telefone</p>
				</div>
				<div id="iconsHeader"></div>
			</div>
		</header>
		<section v-if="contactsList">
			<div v-for="(contact, idx) in filteredcontactsList.length > 0 ? filteredcontactsList : contactsList" :key="idx" :id="'id_'+contact.id" :class="`contactListRow ${(contact.selected ? 'selected' : '')}`">
				<div id="firstRowContactInfo">
					<div id="circleContact">
						<div id="contactCircleBody">
							<div :style="'background-color:'+circleColor[idx > 9 ? String(idx).slice(-1) : idx]">
								<span>{{ contact.name ? contact.name.substr(0, 1).toUpperCase() : '?' }}</span>
							</div>
						</div>
						<div id="contactBody">
							<p>{{contact.name}}</p>
						</div>
					</div>
					<div id="emailBody">
						<p>{{contact.email}}</p>
					</div>
				</div>

				<div id="secondRowContactInfo">
					<div id="phoneBody">
						<p>{{contact.phone}}</p>
					</div>
					<div id="iconsBody">
						<span @click="editContactFn(contact)">
							<img src="../assets/ic-edit.png" srcset="../assets/ic-edit@2x.png 2x, ../assets/ic-edit@3x.png 3x" />
						</span>
						<span @click="deleteContact(contact)">
							<img src="../assets/ic-delete.png" srcset="../assets/ic-delete@2x.png 2x, ../assets/ic-delete@3x.png 3x" />
						</span>
					</div>
				</div>
			</div>
		</section>
		<span v-if="deleteContactValidator && !editContactValidator">
			<DeleteContact @close="deleteContactValidator = $event" @confirmDelete="confirmDelete = $event" />
		</span>
		<span v-if="editContactValidator && !deleteContactValidator">
			<ContactForm :contact="contactToEdit" @close="editContactValidator = $event" @addOrEditContact="editContact = $event" />
		</span>
	</div>
</template>

<script>
import ContactForm from './ContactForm.vue'
import DeleteContact from './DeleteContact.vue'
export default {
	name: 'ContactList',
	components: {
		DeleteContact,
		ContactForm
	},
	props: ['newContact', 'inputSearch', 'setContacts'],
	data() {
		return {
			deleteContactValidator: false,
			confirmDelete: false,
			contactToDelete: '',
			editContactValidator: false,
			editContact: '',
			contactToEdit: '',
			contactsList: [],
			filteredcontactsList: [],
			circleColor: {
				'0': '#e06060',
				'1': '#fa8d68',
				'2': '#90d26c',
				'3': '#68a0fa',
				'4': '#fab668',
				'5': '#8368fa',
				'6': '#fa68b5',
				'7': '#5fe2c4',
				'8': '#f55a5a',
				'9': '#e0de3f'
			}
		}
	},
	beforeMount() {
		if (typeof this.newContact == 'object' && this.setContacts == '') {
			this.contactsList.push(this.newContact)
			this.newContact.removeClassFn(this.newContact, this.contactsList)
		} else {
			this.contactsList = this.setContacts
			this.contactsList = this.contactsList.sort((a, b) => {
				return a.name.localeCompare(b.name)
			})
		}
	},
	watch: {
		confirmDelete() {
			if (this.confirmDelete)
				this.deleteContact()
		},
		editContact() {
			this.contactsList.map((contact, idx) => {
				if (this.editContact.id == contact.id) {
					this.contactsList[idx] = this.editContact
				}
			})

			this.contactsList = this.contactsList.sort((a, b) => {
				return a.name.localeCompare(b.name)
			})
		},
		newContact() {
			this.contactsList.push(this.newContact)

			this.contactsList = this.contactsList.sort((a, b) => {
				return a.name.localeCompare(b.name)
			})
			this.newContact.removeClassFn(this.newContact, this.contactsList)
		},
		inputSearch() {
			this.filteredcontactsList = this.contactsList.filter(ctt => ctt.name.toLowerCase().includes(this.inputSearch.trim().toLowerCase()) ? ctt : '')
		}
	},
	methods: {
		deleteContact(ctt) {
			if (ctt)
				this.contactToDelete = ctt

			if (this.confirmDelete) {
				this.contactsList = this.contactsList.filter(contact => contact.id != this.contactToDelete.id)
				this.confirmDelete = false
				this.deleteContactValidator = false
				this.contactsList.length == 0 ? this.$emit('thereIsNoContact', null) : ''
				return
			}
			this.deleteContactValidator = true
		},
		editContactFn(ctt) {
			this.contactToEdit = ctt
			this.editContactValidator = true
		}
	}

}
</script>

<style scoped>
#firstRowNavBar,
#firstRowContactInfo,
#secondRowNavBar,
#secondRowContactInfo,
#listNavBar,
.contactListRow,
#circleContact,
#contactCircleBody div,
#iconsBody {
	display: flex;
	flex-direction: row;
	align-items: center;
}

.contactListRow p {
	word-break: break-word;
}

#firstRowNavBar,
#firstRowContactInfo {
	width: 60%;
}

#firstRowNavBar > div:last-child {
	margin-left: -3rem;
}
#secondRowNavBar > div:first-child {
	margin-left: -0.5rem;
}

#firstRowNavBar > div,
#firstRowContactInfo > div {
	flex: 1;
}

#secondRowNavBar,
#secondRowContactInfo {
	width: 40%;
}

#secondRowNavBar > div,
#secondRowContactInfo > div {
	flex: 1;
}

#secondRowContactInfo > div:last-child {
	position: absolute;
	right: 1rem;
}

#listNavBar {
	height: 2.5rem;
	padding: 0 1rem 0 2.938rem;
	border-radius: 4px 4px 0 0;
	border: solid 1px var(--white);
	background-color: var(--white-two);
	justify-content: space-between;
}

#listNavBar p {
	font-size: 0.813rem;
	color: var(--bluey-grey);
}

.contactListRow {
	justify-content: space-between;
	min-height: 2.5rem;
	border: solid 1px var(--white);
	border-top: none;
	background-color: var(--white-two);
	font-size: 0.875rem;
	transition: all 200ms;
}
.contactListRow:hover {
	background-color: var(--very-light-pink);
}
.contactListRow:last-child {
	border-radius: 0 0 4px 4px;
}

#circleContact {
	padding: 0 0 0 0.5rem;
}

#contactCircleBody div {
	align-content: center;
	justify-content: center;
	width: 1.5rem;
	height: 1.5rem;
	border-radius: 50%;
	margin: 0 1rem 0 0;
	background-color: #fa8d68;
	color: var(--white-two);
}

#iconsBody span {
	cursor: pointer;
	margin: 0 0.75rem;
}

.selected {
	background-color: var(--very-light-pink) !important;
}

@media (max-width: 479px) {
	.contactListRow {
		flex-direction: column;
		height: auto;
		padding: 0.5rem 0;
		gap: 0.5rem;
	}

	#listNavBar {
		flex-direction: column;
	}

	#firstRowNavBar {
		width: 100%;
		justify-content: space-between;
	}
	#secondRowNavBar {
		width: 100%;
	}

	#firstRowNavBar > div:last-child {
		margin-left: -1rem;
	}
	#secondRowNavBar > div:first-child {
		margin-left: 0;
	}

	#firstRowContactInfo {
		width: 100%;
	}

	#secondRowContactInfo {
		width: 100%;
		padding-left: 0.75rem;
	}

	#secondRowContactInfo > div:last-child {
		position: absolute;
		right: 1rem;
	}
}
</style>
