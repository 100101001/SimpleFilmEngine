<template>
	<div>
		<div class="subject clearfix">

			<h1>
				<span>{{film.title}}</span>
				<span class="year">({{film.pubdate[0].split('-')[0]==''? '未知':film.pubdate[0].split('-')[0]}})</span>
			</h1>

			<div id="mainpic">

				<img width=135 alt="" :src="film.poster" :onerror="logo">

			</div>

			<div id="info" style="text-align: justify">
				<!--导演可能有多位-->
				<span><span class="pl">导演</span>: <span class="attrs">{{directors==''? '未知':directors}}</span></span><br>
				<!--编剧可能有多位-->
				<span>
					<span class="pl">编剧</span>:
					<span class="attrs">{{writers==''? '未知':writers}}</span>
				</span>
				<br>

				<!--主演可能有多位-->
				<span class="actor"><span class="pl">主演</span>: <span class="attrs"><span>{{casts==''? '未知':casts}}
						</span></span></span><br>

				<!--类型可能有多个-->
				<span class="pl">类型:</span> <span property="v:genre">{{genres==''? '未知':genres}}</span><br>

				<span class="pl">制片国家/地区:</span> 中国大陆<br>

				<!--语言可能有多个-->
				<span class="pl">语言:</span> {{languages==''? '未知':languages}}<br>


				<span class="pl">上映日期:</span> <span content="2019-02-05(中国大陆)" property="v:initialReleaseDate">{{pubCountries==''? '未知':pubCountries}}</span><br>
				<span class="pl">片长:</span> <span content="116" property="v:runtime">{{film.duration==''? '未知':film.duration}}分钟</span><br>

				<!--又名可能有多个-->
				<span class="pl">又名:</span> {{aka==''? '无':aka}}<br>

				<span class="pl">IMDb链接:</span> <a :href="imdbLink" target="_blank" rel="nofollow">{{film.imdb}}</a><br>

			</div>


			<div class="related-info" style="margin-bottom:-10px;text-align: justify;">
				<h3>
					剧情简介
				</h3>

				<div class="indent" id="link-report">

					<span>
						　　号称银河系最先进的外星文明试图和地球建交，谁知一连串的误会导致意外发生。外星使者的飞船坠入大气层，最终摔在了中国某市的世界公园中。靠耍猴戏为生的耿浩（黄渤 饰）和酒贩子好友大飞（沈腾
						饰）把受伤的外星人错认为来自南美洲的猴子，在自家猴子受伤的情况下，耿浩开始训练起这个他口中的“刚果骚骚猴”来了。由于失去了超能力加成设备，外星人的本事无法施展，只能任由这两个傻乎乎的地球人打骂操练。尽管如此，他仍试图夺回自己的装备。另一方面，之前与外星人交流失败的超级大国根据外星人留下的信息，穿梭世界各地寻找外星使者。地球的命运朝着不可预测的方向发展……
						<br>
						　　本片创意来自刘慈欣的科幻小说《乡村教师》。
					</span>
					<span class="pl"><a href="https://movie.douban.com/help/movie#t0-qs">©simple film</a></span>

				</div>
			</div>


		</div>
	</div>


</template>

<script>
	export default {
		data() {
			return {
				film: '',
				id: '',
				imdbLink: '',
				logo: 'this.src="' + require('../assets/timg.jpg') + '"',
				directors: '',
				writers: '',
				casts: '',
				genres: '',
				languages: '',
				pubCountries: '',
				aka: ''
			}
		},
		created() {
			console.log(this.$route.params)
			this.id = this.$route.params.id
			this.film = this.$route.params.film
			this.imdbLink = "http://www.imdb.com/title/" + this.film.imdb
			for (var i = 0, len = this.film.directors.length; i < len; i++) {
				if (len <= 5) {
					if (i == 0) {
						this.directors += this.film.directors[i]['name']
					} else {
						this.directors += '/' + this.film.directors[i]['name']
					}
				} else {
					if (i == 0) {
						this.directors += this.film.directors[i]['name']
					} else if (i < 5) {
						this.directors += '/' + this.film.directors[i]['name']
					} else if (i == 5) {
						this.directors += '/更多...'
						break
					}
				}
			}
			for (var i = 0, len = this.film.writers.length; i < len; i++) {
				if (len <= 5) {
					if (i == 0) {
						this.writers += this.film.writers[i]['name']
					} else {
						this.writers += '/' + this.film.writers[i]['name']
					}
				} else {
					if (i == 0) {
						this.writers += this.film.writers[i]['name']
					} else if (i < 5) {
						this.writers += '/' + this.film.writers[i]['name']
					} else if (i == 5) {
						this.writers += '/更多...'
						break
					}
				}
			}
			for (var i = 0, len = this.film.casts.length; i < len; i++) {
				if (len <= 5) {
					if (i == 0) {
						this.casts += this.film.casts[i]['name']
					} else {
						this.casts += '/' + this.film.casts[i]['name']
					}
				} else {
					if (i == 0) {
						this.casts += this.film.casts[i]['name']
					} else if (i < 5) {
						this.casts += '/' + this.film.casts[i]['name']
					} else if (i == 5) {
						this.casts += '/更多...'
						break
					}
				}
			}
			for (var i = 0, len = this.film.genres.length; i < len; i++) {
				if (len <= 5) {
					if (i == 0) {
						this.genres += this.film.genres[i]
					} else {
						this.genres += '/' + this.film.genres[i]
					}
				} else {
					if (i == 0) {
						this.genres += this.film.genres[i]
					} else if (i < 5) {
						this.genres += '/' + this.film.genres[i]
					} else if (i == 5) {
						this.genres += '/更多...'
						break
					}
				}
			}
			for (var i = 0, len = this.film.languages.length; i < len; i++) {
				if (len <= 5) {
					if (i == 0) {
						this.languages += this.film.languages[i]
					} else {
						this.languages += '/' + this.film.languages[i]
					}
				} else {
					if (i == 0) {
						this.languages += this.film.languages[i]
					} else if (i < 5) {
						this.languages += '/' + this.film.languages[i]
					} else if (i == 5) {
						this.languages += '/更多...'
						break
					}
				}
			}

			this.film.pubdate[0] = this.film.pubdate[0].split(')')[0].split('(')[0]
			for (var i = 0, len = this.film.countries.length; i < len; i++) {

				this.film.countries[i] = this.film.countries[i].replace(')', '')
				this.film.countries[i] = this.film.countries[i].replace('(', '')
			}
			for (var i = 0, len = this.film.countries.length; i < len; i++) {
				if (len <= 5) {
					if (i == 0) {

						this.pubCountries += this.film.pubdate[0] + '(' + this.film.countries[i]
					} else {

						this.pubCountries += '/' + this.film.countries[i]
					}
				} else {
					if (i == 0) {

						this.pubCountries += this.film.pubdate[0] + '(' + this.film.countries[i]
					} else if (i < 5) {

						this.pubCountries += '/' + this.film.countries[i]
					} else if (i == 5) {
						this.pubCountries += '/更多...'
						break
					}
				}
			}
			this.pubCountries += ')'
			for (var i = 0, len = this.film.aka.length; i < len; i++) {
				if (len <= 5) {
					if (i == 0) {
						this.aka += this.film.aka[i]
					} else {
						this.aka += '/' + this.film.aka[i]
					}
				} else {
					if (i == 0) {
						this.aka += this.film.aka[i]
					} else if (i < 5) {
						this.aka += '/' + this.film.aka[i]
					} else if (i == 5) {
						this.aka += '/更多...'
						break
					}
				}
			}
			//console.log(this.pubCountries)

		}
	}
</script>

<style>
	html body,
	html td,
	html th,
	html .pl,
	html input {
		font-size: 16px;
	}

	h1 .year {
		color: #888;
	}

	.year {
		display: inline-block;
		zoom: 1;
	}

	.subject #mainpic {
		margin-right: 15px;
	}

	#mainpic {
		margin: 3px 0 0 0;
		float: left;
		text-align: center;
		margin: 3px 12px 0 0;
		max-width: 155px;
		overflow: hidden;
	}

	a:link {
		color: #37a;
		text-decoration: none;
	}

	#info {
		max-width: 333px;
	}

	#info {
		float: left;
		max-width: 248px;
		word-wrap: break-word;
		margin-right: 2rem
	}

	.pl {
		font: 12px Arial, Helvetica, sans-serif;
		line-height: 150%;
		color: #666666;
	}

	.clearfix:after {
		content: ".";
		display: block;
		height: 0;
		clear: both;
		visibility: hidden;
	}

	.indent {
		*zoom: 1;
		margin-bottom: 30px;
	}

	.indent {
		word-break: break-all;
	}

	.related-info {
		width: 10;
		/* border:1px solid #DDDDDD; */
		border-radius: 5px 5px;
		/* margin-left:2rem */
	}
</style>
