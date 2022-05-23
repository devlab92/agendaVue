<template>
	<div id="newContact">
		<div>
			<img src="../assets/ic-plus.png" srcset="../assets/ic-plus@2x.png 2x, ../assets/ic-plus@3x.png 3x" />
			<span class="text-style-3">Criar contato</span>
		</div>
	</div>
</template>

<script>
export default {
	name: 'NewContactButton',
}
</script>

<style scoped>
#newContact {
	width: 9rem;
	border-radius: 20px;
	box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.16),
		0 0 0 0.5px var(--black-8), inset 0 0 0 0.5px var(--black-8),
		0 2px 4px 0.5px rgba(0, 0, 0, 0.16);
	background-color: var(--light-yellowish-green);
	cursor: pointer;
}

#newContact div {
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-items: center;
	padding: 0.5rem 1rem;
}

#newContact img {
	width: 1rem;
	height: 1rem;
	margin: 0 0.5rem 0 0;
	object-fit: contain;
}

@media (max-width: 479px) {
	#newContact{
		width: 100%;
		max-width: 9rem;
	}
	span{
		font-size: .8em;
	}
		#newContact img {
			width: .75rem;
			height: .75rem;
			margin: 0 .25rem 0 0;
		}
}
</style>
