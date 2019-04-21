<template>
	<div class="hello">
		<p class="ul"></p>
		<table width="100%">
			<tbody>
				<tr class="item">
					<td width="100" valign="top">


						<a title="" class="nbg" href="javascript:void(0)" @click="Describe">
							<img width="75" alt="" :src="film.poster" :onerror="logo" >
						</a>
					</td>

					<td valign="top">


						<div class="pl2">
							<a title="" class="nbg" href="javascript:void(0)" @click="Describe">
								<p style="font-size:13px;">{{film.title}}</p>
							</a>
							<!--上映时间-->
							<div style="margin-bottom: 1em;">
								<p>
									<span class="pl">
										{{film.summary.substr(0,100)+'....'}}
									</span>
								</p>
							</div>

							<!--评分-->
							<div class="star clearfix">
								<!-- <span class="allstar20"></span> -->
								<el-col :span="6" :offset="6">
									<el-rate style="float: right;" v-model="film.rating.average/2" disabled show-score text-color="#ff9900"></el-rate>
								</el-col>
								<el-col :span="6"> <span class="pl" style="float: left;margin-left:1rem;">({{film.rating.rating_people==''? 0:film.rating.rating_people}}人评价)</span></el-col>
								<!-- <span class="rating_nums">{{film.rating.average}}分</span> -->

							</div>

						</div>
					</td>

				</tr>
			</tbody>
		</table>
	</div>
</template>

<script>
	export default {
		name: 'FilmCell',
		props: ['films'],
		data() {
			return {
				film: JSON.parse(this.films),
				logo: 'this.src="' + require('../assets/timg.jpg') + '"'
			}; //重新赋值？
		},
		watch: {
			films(newValue, oldValue) {
				this.film = JSON.parse(newValue) //监听
			}
		},
		methods:{
			Describe(){
				this.$parent.getDescribe(this.film,this.film._id)
			},
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	/* @import '../static/css/cell_template.css' */
	.ul {
		border-bottom: 1px dashed #DDDDDD;
		line-height: 100%;
		clear: both;
	}

	tr {
		display: table-row;
		vertical-align: inherit;
		border-color: inherit;
	}

	.pl2 {
		font: 14px Arial, Helvetica, sans-serif;
		line-height: 150%;
		color: #666666;
	}

	/* .pl {
		white-space: normal;
		font-size: 13px;
	} */

	.clearfix {
		display: block;
	}


	a {
		cursor: pointer;
		color: #37a;
		text-decoration: none;
	}

	.rating_nums {
		padding-left: 0;
	}

	.rating_nums,
	.rating_num {
		color: #e09015;
		font-size: 12px;
		padding: 0 3px;
	}

	.pl {
		font: 12px Arial, Helvetica, sans-serif;
		line-height: 150%;
		color: #666666;
	}
</style>
