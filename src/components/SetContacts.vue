<template>
	<div id="setContacts">
		<div>
			<img src="../assets/ic-plus.png" srcset="../assets/ic-plus@2x.png 2x, ../assets/ic-plus@3x.png 3x" />
			<span class="text-style-3">Vários contatos</span>
		</div>
	</div>
</template>

<script>
export default {
	name: 'SetContactsButton'
}
</script>

<style scoped>
#setContacts {
	margin: 0.75rem 0 0 0;
	width: 100%;
	max-width: 10rem;
	border-radius: 20px;
	box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.16),
		0 0 0 0.5px var(--black-8), inset 0 0 0 0.5px var(--black-8),
		0 2px 4px 0.5px rgba(0, 0, 0, 0.16);
	background-color: var(--light-yellowish-green);
	cursor: pointer;
}

#setContacts div {
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-items: center;
	padding: 0.5rem 1rem;
}

#setContacts img {
	width: 1rem;
	height: 1rem;
	margin: 0 0.5rem 0 0;
	object-fit: contain;
}

@media (max-width: 479px) {
	span {
		font-size: 0.8em;
	}
	#setContacts img {
		width: 0.75rem;
		height: 0.75rem;
		margin: 0 0.25rem 0 0;
	}
}
</style>
