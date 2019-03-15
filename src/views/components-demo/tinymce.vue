<template>
	<section>
		<!--工具条-->
		<el-col :span="24" class="toolbar" style="padding-bottom: 0px;">
			<el-form :inline="true" :model="filters">
				<el-form-item>
					<el-select v-model="value4" clearable placeholder="请选择">
						<el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
						</el-option>
					</el-select>
				</el-form-item>
				<el-form-item>
					<el-input v-model="filters.name" placeholder="姓名"></el-input>
				</el-form-item>
				<el-form-item>
					<el-button type="primary" v-on:click="getUsers">查询</el-button>
				</el-form-item>

			</el-form>
		</el-col>

		<!--列表-->
		<el-table :data="userList" highlight-current-row v-loading="listLoading" @selection-change="selsChange" style="width: 100%;">
			<el-table-column type="selection" width="55">
			</el-table-column>
			<el-table-column type="index" label="编号" width="70">
			</el-table-column>
			<el-table-column prop="id" label="客戶编号" v-if="false" width="120">
			</el-table-column>
			<el-table-column prop="name" label="客戶姓名" width="110">
			</el-table-column>
			<el-table-column prop="sex" label="性别" :formatter="formatSex" width="100">
			</el-table-column>
			<el-table-column prop="age" label="年龄" width="100">
			</el-table-column>
			<!--
			<el-table-column prop="phone" label="联系方式" width="200">
			</el-table-column>-->
			<el-table-column prop="address" label="地址" min-width="150">
			</el-table-column>
			<el-table-column prop="callId" label="拨打记录" v-if="false" min-width="140">
			</el-table-column>
			<el-table-column prop="isEnabled" label="" min-width="150">
			</el-table-column>

			<el-table-column label="操作" width="250">
				<template scope="scope">
					<el-button size="small" @click="handleEdit(scope.$index, scope.row)">拨打电话</el-button>
					<el-button type="danger" size="small" :disabled="scope.row.callId == ''" @click="addcallSubmit(scope.$index, scope.row)">查看结果</el-button>
				</template>
			</el-table-column>
		</el-table>
		<!--<div align="center">
			<el-pagination @size-change="handleSizeChange" @current-change="handleCurrentChange" :current-page="currentPage" :page-sizes="[10, 20, 30]" :page-size="pagesize" layout="total, sizes, prev, pager, next, jumper" :total=parseInt(total)>
			</el-pagination>
		</div>-->

		<!--工具条-->
		<!--<el-col :span="24" class="toolbar">

			<el-pagination layout="prev, pager, next" @current-change="handleCurrentChange" :page-size="20" :total="total" style="float:right;">
			</el-pagination>
		</el-col>-->
		<!--拨打界面-->
		<el-dialog title="编辑" v-model="editFormVisible" :close-on-click-modal="false">
			<el-form :model="editForm" label-width="80px" :rules="editFormRules" ref="editForm">
				<el-form-item label="手机号码" prop="phone" >
					<el-input v-model="editForm.phone" auto-complete="off"></el-input>
				</el-form-item>

			</el-form>
			<div slot="footer" class="dialog-footer">
				<el-button @click.native="editFormVisible = false">取消</el-button>
				<el-button type="primary" @click.native="editSubmit" :loading="editLoading">提交</el-button>
			</div>
		</el-dialog>

	</section>
</template>

<script>
import Tinymce from '@/components/Tinymce'

import axios from 'axios'

	export default {
		data() {
			return {
				filters: {
					name: ''
				},
				options: [{
					value: '选项1',
					label: '车险'
				}, {
					value: '选项2',
					label: '意外伤害险'
				}, {
					value: '选项3',
					label: '健康保险'
				}, {
					value: '选项4',
					label: '人寿保险'
				}, {
					value: '选项5',
					label: '财产保险'
				}],
				value4: '',
				userList: [],
				currentPage: 1,
				pageSize: 30,
				currentTotal: 0,
				listLoading: false,
				sels: [], //列表选中列

				editFormVisible: false, //编辑界面是否显示
				editLoading: false,
				editFormRules: {
					name: [{
						required: true,
						message: '请输入姓名',
						trigger: 'blur'
					}]
				},
				//拨打界面数据
				editForm: {
					phone: ''
				},

			}
		},

		methods: {
			// 计算当前页面的数据
			tableList() {
				// this.displayData是当前页面要显示的数据
				this.displayData = []
				for(　　　　 // pagesize是当前页面要显示总条数，例如：每页显示20条；currentPage是当前页面数;
					var j = this.pagesize * (this.currentPage - 1); j < this.pagesize * this.currentPage; j++) {
					// this.gameNum是总数据  
					if(this.gameNum[j]) {
						this.displayData.push(this.gameNum[j])
					}
				}
			},

			// 获取当前页
			paginCurrentChange(page) {
				this.currentPage = page;
				this.tableList();
			},
			
			//性别显示转换
			formatSex: function(row, column) {
				return row.sex == 1 ? '男' : row.sex == 0 ? '女' : '未知';
			},

			//获取用户列表
			getUsers() {
				var vm = this;
				axios.get('/api/call/getdialqueue')
					.then(function(response) {
						vm.userList = response.data
					})
			},
			//显示拨打界面
			handleEdit: function(index, row) {
				this.editFormVisible = true;
				this.editForm = Object.assign({}, row);
			},
			//拨打
			editSubmit() {
				this.$refs.editForm.validate((valid) => {
					if(valid) {
							this.editLoading = true;
							//NProgress.start();
							let para = Object.assign({}, this.editForm);
							para.phone = /^1[34578]\d{9}$/;
							var vm = this;

							axios.post("/api/call/addcall", {
								'customerId': para.id,
								'phone': vm.editForm.phone
							}).then((response) => {
								let res = response.data;
								this.$message({
									message: '拨打成功',
									type: 'success'
								});

								console.log(res);
								vm.editLoading = false;
								this.editFormVisible = false;
								vm.getUsers();
							});

							/*axios.get('http://112.64.145.218:3083/call/addcall?callId=this.id')
								.then(function(response) {
									this.editLoading = false;
									//NProgress.done();
									this.$message({
										message: '拨打成功',
										type: 'success'
									});
									this.$refs['editForm'].resetFields();
									this.editFormVisible = false;
									this.getUsers();
								})*/
					}
				});
			},
			addcallSubmit: function(index, row) {
				 this.$router.push({ path:'/markdown',query: {
						id: row.callId
					} })
				
			},

			selsChange: function(sels) {
				this.sels = sels;
			}
		},
		mounted() {
			this.getUsers();
		},
		created() {}
}
</script>

<style scoped>
.editor-content{
  margin-top: 20px;
}
</style>

