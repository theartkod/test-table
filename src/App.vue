<template>
	<div id="app">
		<div class="container">
			<div class="row">
				<div class="col-lg-12">
					<div class="title">Выбрано элементов: {{checked.length}}</div>
					<div class="wrapp-table">
						<table class="table">
							<thead>
							<tr class="table__head">
								<th></th>
								<th>Имя и фамилия</th>
								<th>Телефон</th>
								<th class="table__head--last">Дата</th>
							</tr>
							</thead>
							<tbody>
							<tr class="table-row" v-for="item in tableData">
								<td class="table-row__column table-row__column--first">
									<ui-checkbox @change="isChecked()" v-model="arrCheck[item.id]"></ui-checkbox>
								</td>
								<td class="table-row__column">
									<textarea class="table-row-input" placeholder="Иван Иванов">{{item.name}} {{item.lastname}}</textarea>
								</td>
								<td class="table-row__column">
									<textarea class="table-row-input" placeholder="Телефон">{{item.phone}}</textarea>
								</td>
								<td class="table-row__column table-row__column--last">{{item.date}}</td>
							</tr>
							</tbody>
						</table>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import axios from 'axios'
	import UiCheckbox from 'keen-ui/lib/UiCheckbox.min'
	export default {
		name: 'app',
		components: {UiCheckbox},
		data () {
			return {
				tableData: [],
				checked: [],
				arrCheck: []
			}
		},
		methods: {
			loadData: function () {
				axios.get('//www.filltext.com/?rows=10&name={firstName}&lastname={lastName}&date={date}&phone={phone}&id={index}')
					.then((res) => {
						this.tableData = res.data
					})
			},
			isChecked: function () {
				this.checked = this.arrCheck.filter(function (item) {
					return item === true
				})
			}
		},
		created: function () {
			this.loadData()
		}
	}
</script>

<style>
	body {
		background-color: #EEEEEE;
	}

	.wrapp-table {
		box-shadow: 0 3px 5px 0 #AEAEAE;
		border-radius: 4px;
		overflow: hidden;
		border: 1px solid #AEAEAE;
		background-color: #fff;
		overflow-x: auto;
	}

	.table {
		width: 100%;
	}

	.table-row {
		height: 60px;
		border-top: 1px solid #E5E5E5;
	}

	.table__head {
		height: 60px;
		border-top: 1px solid #E5E5E5;
		color: #787878;
	}

	.table-row-input {
		border: none;
		outline: none;
		height: 24px;
		overflow: hidden;
		resize: none;
		opacity: .7;
	}

	.table-row-input:hover {
		opacity: 1;
	}

	.table-row-input:focus {
		outline: none;
		opacity: 1;
	}

	.table-row__column--first {
		padding-left: 30px;
		padding-top: 9px;
	}

	.table-row__column--last {
		text-align: right;
		padding-right: 30px;
	}

	.table__head--last {
		text-align: right;
		padding-right: 30px;
	}

	.title {
		padding: 15px 0;
	}
</style>
