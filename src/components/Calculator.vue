<template>
	<div>
		<input type="number" v-model.number="operand1"><input type="number" v-model.number="operand2"> = {{ result }}
		<h1 v-if="operand2 == 0">На ноль делить нельзя!</h1>
		<div>
			<button @click="sum">+</button>
			<button @click="minus">-</button>
			<button v-on:click="multi">*</button>
			<button @click="division">/</button>
			<button @click="divisionFull">divisionFull</button>
			<button @click="pow">pow</button>
			<button @click="clear">clear</button>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'Calculator',
		data: () => ({
			operand1: Number,
			operand2: Number,
			result: 0
		}),
		methods: {
			sum() {
				return this.result = this.operand1 + this.operand2;
			},
			minus() {
				return this.result = this.operand1 - this.operand2;
			},
			multi() {
				return this.result = this.operand1 * this.operand2;
			},
			division() {
				if (this.operand2 != 0) {
					return this.result = this.operand1 / this.operand2;
				}
			},
			pow() {
				this.result = this.operand1;

				for (let i = 1; i < this.operand2; i++) {
					this.result *= this.operand1;
				}

				return this.result;
			},
			divisionFull() {
				if (this.operand2 != 0) {
					return this.result = parseInt(this.operand1 / this.operand2);
				}
			},
			clear() {
				this.operand1 = 0;
				this.operand2 = 0;
				return this.result = 0;
			}
		}
	}
</script>