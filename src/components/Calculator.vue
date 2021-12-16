<template>
	<div>
		<div>
			<label for="keybord">Отобразить экранную клавиатуру</label>
			<input type="checkbox" v-model="showKeybord" id="keybord">
		</div>
		<div v-show="showKeybord">
			<button v-for="btn in collection" :key="btn" @click="addNumber(btn)">{{btn}}</button>
			<button @click="removeSymbol">clear</button>
		</div>
		<div>
			<label for="operand1">Операнд 1</label>
			<input type="radio" id="operand1" v-model="picked" value="operand1">
			<label for="operand2">Операнд 2</label>
			<input type="radio" id="operand2" v-model="picked" value="operand2">
		</div>
		<input type="number" v-model.number="operand1"><input type="number" v-model.number="operand2"> = {{ result }}
		<div v-show="error" class="error">{{ error }}</div>
		<div>
			<button v-for="operation in operations"
			@click="calculate(operation)"
			:key="operation"
			:title="operation" >{{ operation }}</button>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'Calculator',
		data: () => ({
			showKeybord: true,
			picked: '',
			operations: ['+', '-', '*', '/', 'pow', 'divisionFull', 'clearFields' ],
			collection: [0,1,2,3,4,5,6,7,8,9],
			operand1: 0,
			operand2: 0,
			result: 0,
			error: ''
		}),
		methods: {
			calculate(operation) {
				this.error = '';
				const calcOperations = {
					'+': () => this.operand1 + this.operand2,
					'-': () => this.operand1 - this.operand2,
					'*': () => this.operand1 * this.operand2,
					'/': () => {
						const { operand1, operand2 } = this;
						if (operand2 === 0) {
							this.error = 'На ноль делить нельзя!';
							return this.result = 0;
						} else {
							return operand1 / operand2;
						}
					},
					'pow': () => {
						this.result = this.operand1;
						for (let i = 1; i < this.operand2; i++) {
							this.result *= this.operand1;
						}
						return this.result;
					},
					'divisionFull': () => parseInt(this.operand1 / this.operand2),
					'clearFields': () => {
						this.operand1 = 0;
						this.operand2 = 0;
						return this.result = 0;
					}
				}
				this.result = calcOperations[operation]();
			},
			addNumber(btn) {
				if (this.picked == 'operand1') {
					this.operand1 += '' + btn;
					this.operand1 = Number(this.operand1);
				}
				if (this.picked == 'operand2') {
					this.operand2 += '' + btn;
					this.operand2 = Number(this.operand2);
				}
			},
			removeSymbol() {
				if (this.picked == 'operand1') {
					let string = '';
					this.operand1 = String(this.operand1);
					string = this.operand1;
					string = string.split('').slice(0, string.length - 1).join('');
					this.operand1 = Number(string);
				}
				if (this.picked == 'operand2') {
					let string = '';
					this.operand2 = String(this.operand2);
					string = this.operand2;
					string = string.split('').slice(0, string.length - 1).join('');
					this.operand2 = Number(string);
				}
			}
		}
	}
</script>

<style scoped="scss">
	.error {
		color: red;
		padding: 10px 0;
	}
</style>