<template>
	<div class="manage tc">
		<div class="center-box">
			<button @click="add">新增</button>
			<div class="input-area" v-show='showAdd'>
				<input type="text" placeholder="请输入人员姓名" v-model="nameValue"  @keyup.13="addName">
				<button @click="addName">确定</button>
			</div>
			<table>
				<tr>
					<th>姓名</th>
					<th>操作</th>
				</tr>
				<tr v-for="(item,index) in peooles">
					<td :class="{'action':item.isBool}">
						<p>{{item.name}}</p>
						<input @keyup.13 ="determine" v-model='newName'>
					</td>
					<td :id="index">
						<span @click='edit(index)'>编辑</span>
						<span @click='del(index)'>删除</span>
					</td>
				</tr>
			</table>
		</div>
		<footer-nav :class="{'isManage':isNowPage}"></footer-nav>
	</div>
</template>
<style scoped>
	.center-box {
		width: 500px;
		margin: 0 auto;
	}
	.manage button {
		height: 30px;
		width:150px;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 20px;
		color: #fff;
		background: #42b983;
		margin: 10px auto;
		border-radius: 10px;
	}
	.input-area  {
		display: flex;
		align-items: center;
	}
	.input-area input {
		height: 35px;
		flex: 1;
		padding-left: 15px;
		border:1px solid #ccc;
	}	
	.input-area button {
		height: 35px;
		margin-left: 20px;
		width: 70px;
	}
	table {
		width: 500px;
	}
	table tr {
		border-bottom: 1px solid #000;
		height: 50px;
		background: #ddd;
	}
	table td span{
		cursor: pointer;
	}
	table td p {
		display: block;
	}
	table td input {
		height: 50px;
		width: 100%;
		font-size: 20px;
		display: none;
	}
	table td.action input{
		display: block;
	}
	table td.action p{
		display: none;
	}
</style>
<script>
	import FooterNav from '../../components/footer'
	export default {
		components:{
			FooterNav
		},
		data(){
			return {
				isNowPage:true,		// 底部显示选中的class
				showAdd:false,		// 是否显示新增的人员的input
				peooles:[
							{"name":"测试1","isBool":false},
							{"name":"测试2","isBool":false}
						],
				nameValue:"",
				editId:0,
				newName:"",
				mun:[]
			}
		},
		methods:{
			add(){
				this.showAdd = !this.showAdd?true:false
			},
			addName(){	// 增加人员列表
				var v = this.nameValue;
				if(v.trim() == ""){
					alert("请输入新增人员的姓名")
				}else{
					var data = {};
					data.name = v;
					this.peooles.push(data)
				}
				this.nameValue = "";
			},
			del(index){	// 删除
				this.peooles.splice(index,1)
			},
			edit(index){	// 编辑
				this.editId = index;
				this.peooles.map( function(item) {
					item.isBool = false;
				});
				this.peooles[index].isBool = true;
				this.newName = this.peooles[index].name;
			},
			determine(){ // 编辑完成
				this.peooles[this.editId].name = this.newName;
				this.peooles[this.editId].isBool = false;	
			}
		}
	}
</script>