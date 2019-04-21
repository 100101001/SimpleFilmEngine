<template>
	<div>
		<!-- 标语 -->
		<header style="margin-bottom=1rem">
			<h1 >CHECK YOUR FAVORITE FILM AT SIMPLE FILM</h1>
		</header>
		
		<!-- 搜索栏 -->
		<nav>
			<el-row>
				<el-col :span='5' :offset='10'><el-input style="float:right"  v-model="filmTitle" placeholder="请输入电影名"></el-input></el-col>
				<el-col :span='6'><el-button style="float:left;margin-left:1rem"  icon="el-icon-search" circle @click="searchBytitle"></el-button></el-col>
			</el-row>
		</nav>
		
		<!-- 电影列表 -->
		<FilmCell v-for="item in currentFilms" :films="item" @click="getDescribe()">
		</FilmCell>

		<!-- 分页器 -->
		<el-pagination style="margin-top: 1rem;" @current-change="handleCurrentChange" :page-size="10" :current-page="currentPage"
		 background layout="prev, pager, next" :total="200">
		</el-pagination>
	</div>
</template>

<script>
	import axios from 'axios'

	import FilmCell from './FilmCell';
	import Describe from './FilmCellDetail';

	export default {
		name: 'App',
		components: {
			FilmCell
		},
		data() {
			return {
				films: '',
				currentPage: 1,
				filmTitle:'',
				currentFilms:[]
			};
		},
		created: function() {
			//初始化电影列表数据
			axios.get('../../static/resources/films2.json').then(response =>
				(this.films = response.data,this.currentFilms=this.films.slice(10 * (this.currentPage - 1), 10 * this.currentPage))
			)
		},
		mounted: function() {

		},
		methods: {
			handleCurrentChange(val) {
				this.currentPage = val
				this.currentFilms=this.films.slice(10 * (this.currentPage - 1), 10 * this.currentPage)
			},
			getDescribe(film, id) {

				this.$router.push({
					name: 'Describe',
					params: {
						id: id,
						film: film
					}
				})

			},
			searchBytitle(){
				//this.filmTitle;
				
				var serachResult=[];
				var input=this.filmTitle.trim()
				for(var i=0,len=this.films.length;i<len;i++){
					var film=JSON.parse(this.films[i])
					if (film.title){
						var s=film.title.trim().toUpperCase()
						input=input.toUpperCase()
						if(s.indexOf(input)!=-1){
							serachResult.push(this.films[i])
						}
					}
					
				}
				this.currentFilms=serachResult
			}
		}
	}
</script>

<style>
	.nav-search .inp input {
		background: #fff;
		width: 96%;
		margin: 0;
		text-align: left;
		height: 30px;
		padding-left: 10px;
		height: 28px\9;
		line-height: 28px\9;
		outline: none;
	}
</style>
