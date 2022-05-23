<template>
	<div id="modal">
		<div id="modalBox">
			<div id="modalHeader">
				<p>Excluir o contato</p>
			</div>
			<hr />
			<div id="modalBody">
				<div>
					<p>Deseja realmente excluir o contato?</p>
				</div>
			</div>
			<hr />
			<div id="modalFooter">
				<div id="cancel" @click="close()">
					<p>Cancelar</p>
				</div>
				<div id="save" @click="confirm()">
					<div>
						<p>Excluir</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'DeleteContact',
	methods: {
		close() {
			this.$emit('close', false)
		},
		confirm() {
			this.$emit('confirmDelete', true)
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
	height: 5.781rem;
}

#modalBody div {
	margin: 10px;
}

#modalBody p {
	margin: 0 0 0.25em 0;
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

@media (max-width: 479px) {
	#modalFooter {
		width: 100%;
		margin: 0;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		gap: 0.25rem;
	}
	#modalFooter > div:first-child {
		margin: 0;
	}
}
</style>
