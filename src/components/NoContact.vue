<template>
	<div id="noContact">
		<div>
			<img src="../assets/ic-book.png" srcset="../assets/ic-book@2x.png 2x, ../assets/ic-book@3x.png 3x" />
			<p class="Text-Style">Nenhum contato foi criado ainda.</p>
		</div>
	</div>
</template>

<script>
export default {
	name: 'NoContact',
	components: {
	}

}
</script>

<style scoped>
#noContact {
	margin: 10rem 0 0 0;
}
#noContact div {
	display: flex;
	flex-direction: column;
	align-items: center;
}

#noContact img {
	width: 100%;
	height: auto;
	max-width: 14.813rem;
	margin: 0 0 1.5rem 0.063rem;
}

#noContact p {
	margin: 0 0 1.5rem 0;
	color: var(--dark);
}
</style>
