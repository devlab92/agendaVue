<template>
	<div id="app">
		<header id="navBar">
			<div id="logoBtn">
				<div id="ubookLogo">
					<img src="./assets/ic-logo.png" srcset="./assets/ic-logo@2x.png 2x, ./assets/ic-logo@3x.png 3x" alt="Logo da Ubook" />
				</div>
				<div id="newUserButton">
					<span @click="formValidator = !formValidator">
						<NewContactButton />
					</span>
				</div>
			</div>
			<div id="searchInput">
				<input type="text" v-model="inputSearch" class="text-style-2" placeholder="Buscar..." />
			</div>
		</header>

		<section>
			<span v-if="contact || setContacts">
				<ContactList :newContact="contact" :setContacts="setContacts" :inputSearch="inputSearch" @thereIsNoContact="contact = $event" />
			</span>
			<span v-else id="noCantactSection">
				<NoContact @formValidator="formValidator = $event" />
				<span @click="formValidator = !formValidator">
					<NewContactButton />
				</span>
				<span @click="setContactsFn()">
					<SetContactsButton />
				</span>
			</span>

			<span v-if="formValidator">
				<ContactForm @close="formValidator = $event" @addOrEditContact="contact = $event" />
			</span>
		</section>
	</div>
</template>

<script>
import NewContactButton from './components/NewContactButton.vue'
import SetContactsButton from './components/SetContacts.vue'
import NoContact from './components/NoContact.vue'
import ContactForm from './components/ContactForm.vue'
import ContactList from './components/ContactList.vue'
export default {
	name: 'App',
	components: {
		NewContactButton,
		SetContactsButton,
		NoContact,
		ContactForm,
		ContactList
	},
	data() {
		return {
			inputSearch: '',
			formValidator: false,
			contact: '',
			setContacts: ''
		}
	},
	methods: {
		setContactsFn() { 
			let removeClass = function (contact, contactsList) {
				setTimeout(() => {
					let element = document.getElementById('id_' + contact.id)
					if (element) {
						element.classList.remove('selected')
						delete contactsList.find(ctt => ctt.id == contact.id).selected
					}
				}, 10000)}

			this.setContacts = [
				{id: 100, name: 'Diana', email: 'diana@mail.com', phone: '(11) 98432-9263', removeClassFn: removeClass},
				{id: 101, name: 'Alana', email: 'alana@mail.com', phone: '(11) 98432-9263', removeClassFn: removeClass},
				{id: 102, name: 'Carlos', email: 'carlos@mail.com', phone: '(11) 98432-9263', removeClassFn: removeClass},
				{id: 103, name: 'Fabio', email: 'fabio@mail.com', phone: '(11) 98432-9263', removeClassFn: removeClass},
				{id: 104, name: 'Homero', email: 'homero@mail.com', phone: '(11) 98432-9263', removeClassFn: removeClass},
				{id: 105, name: 'George', email: 'george@mail.com', phone: '(11) 98432-9263', removeClassFn: removeClass},
				{id: 106, name: 'Elane', email: 'elane@mail.com', phone: '(11) 98432-9263', removeClassFn: removeClass},
				{id: 107, name: 'Bianca', email: 'bianca@mail.com', phone: '(11) 98432-9263', removeClassFn: removeClass}
			]
			
		}
	}
}
</script>

<style>
body {
	margin: 0;
	padding: 0;
	background-color: #f8f9fd;
	padding: 1rem;
	font-family: Roboto;
}

p {
	margin: 0;
	padding: 0;
}

#navBar {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin: 0 0 1rem 0;
}

#logoBtn {
	width: 100%;
	display: flex;
	flex-direction: row;
}

#ubookLogo {
	max-width: 9.25rem;
	height: auto;
	margin-right: 3.75rem;
}

#ubookLogo img {
	width: 100%;
	height: auto;
	max-width: 9.25rem;
}

#searchInput {
	width: 100%;
}

#searchInput input {
	width: -webkit-fill-available;
	height: 2rem;
	margin: 0 0 0 1.5rem;
	padding: 0.438rem 0.5rem 0.375rem;
	border-radius: 4px;
	background-color: var(--pale-grey);
	background-image: url("./assets/ic-search.png");
	background-repeat: no-repeat;
	background-position-x: calc(100% - 0.5rem);
	background-position-y: center;
	border: none;
}

#searchInput input:focus {
	box-shadow: 0 0 0 0;
	border: 0 none;
	outline: 0;
}

#searchInput input::placeholder {
	font-family: Roboto;
	font-size: 1rem;
	font-weight: normal;
	font-stretch: normal;
	font-style: normal;
	line-height: normal;
	letter-spacing: normal;
	color: var(--bluey-grey);
}

#noCantactSection {
	display: flex;
	flex-direction: column;
	align-items: center;
}

@media (max-width: 767px) {
	#navBar {
		flex-direction: column;
		gap: 1rem;
	}

	#searchInput input {
		margin: 0;
	}
}

@media (max-width: 479px) {
	#logoBtn {
		gap: 1rem;
		flex-direction: column;
		align-items: center;
	}

	#ubookLogo {
		margin-right: 0;
	}
}

@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap");

.text-style {
	font-family: Roboto;
	font-size: 1rem;
	font-weight: normal;
	font-stretch: normal;
	font-style: normal;
	line-height: normal;
	letter-spacing: normal;
	text-align: center;
	color: var(--dark);
}
.text-style-2 {
	font-family: Roboto;
	font-size: 1rem;
	font-weight: normal;
	font-stretch: normal;
	font-style: normal;
	line-height: normal;
	letter-spacing: normal;
	color: var(--bluey-grey);
}
.text-style-3 {
	font-family: Roboto;
	font-size: 0.875rem;
	font-weight: 500;
	font-stretch: normal;
	font-style: normal;
	line-height: normal;
	letter-spacing: normal;
	color: #fa7268;
}

:root {
	--sky-blue: #68a0fa;
	--pale-olive-green: #90d26c;
	--dark: #2a2d3b;
	--bluey-grey: #9198af;
	--light-yellowish-green: #dbff90;
	--white-two: #fff;
	--white: #e1e1e1;
	--very-light-pink: #fff3f2;
	--pale-grey: #e4e7f4;
	--black-8: rgba(0, 0, 0, 0.08);
}
</style>
