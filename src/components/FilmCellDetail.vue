<template>
  <div>
    <div class="subject clearfix">
      <h1>
        <span>{{film.title}}</span>
        <span
          class="year"
        >({{film.pubdate[0].split('-')[0]==''? '未知':film.pubdate[0].split('-')[0]}})</span>
      </h1>

      <div id="mainpic" style="margin-left:5rem;">
        <img width="135" alt :src="film.poster" :onerror="logo">
      </div>

      <div id="info" style="text-align: justify">
        <!--导演可能有多位-->
        <span>
          <span class="pl" style="color:#909399">
            <strong>导演:</strong>
          </span>
          <span class="attrs">{{directors==''? '未知':directors}}</span>
        </span>
        <br>
        <!--编剧可能有多位-->
        <span>
          <span class="pl" style="color:#909399">
            <strong>编剧:</strong>
          </span>
          <span class="attrs">{{writers==''? '未知':writers}}</span>
        </span>
        <br>

        <!--主演可能有多位-->
        <span class="pl" style="color:#909399">
          <strong>主演:</strong>
        </span>
        <span class="attrs">
          <span>{{casts==''? '未知':casts}}</span>
        </span>
        <br>

        <!--类型可能有多个-->
        <span class="pl" style="color:#909399">
          <strong>类型:</strong>
        </span>
        <span property="v:genre">{{genres==''? '未知':genres}}</span>
        <br>

        <!--语言可能有多个-->
        <span class="pl" style="color:#909399">
          <strong>语言:</strong>
        </span>
        {{languages==''? '未知':languages}}
        <br>

        <span class="pl" style="color:#909399">
          <strong>上映日期:</strong>
        </span>
        <span
          content="2019-02-05(中国大陆)"
          property="v:initialReleaseDate"
        >{{pubCountries==''? '未知':pubCountries}}</span>
        <br>
        <span class="pl" style="color:#909399">
          <strong>片长:</strong>
        </span>
        <span content="116" property="v:runtime">{{film.duration==''? '未知':film.duration}}分钟</span>
        <br>

        <!--又名可能有多个-->
        <span class="pl" style="color:#909399">
          <strong>又名:</strong>
        </span>
        {{aka==''? '无':aka}}
        <br>

        <span class="pl" style="color:#909399">
          <strong>IMDb链接:</strong>
        </span>
        <a :href="imdbLink" target="_blank" rel="nofollow">{{film.imdb}}</a>
        <br>
      </div>

      <div class="related-info" style="margin-bottom:-10px;text-align: justify;">
        <h3>剧情简介</h3>

        <div class="indent" id="link-report">
          <span>{{film.summary}}</span>
          <span class="pl">
            <a href="https://github.com/100101001/a_simplefilm">©simple film</a>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name:"FilmCellDetail",
  data() {
    return {
      film: "",
      id: "",
      imdbLink: "",
      logo: 'this.src="' + require("../assets/timg.jpg") + '"',
      directors: "",
      writers: "",
      casts: "",
      genres: "",
      languages: "",
      pubCountries: "",
      aka: ""
    };
  },
  created() {
    //console.log(this.$route.params);
    this.id = this.$route.params.id;
    this.film = this.$route.params.film;
    this.imdbLink = "http://www.imdb.com/title/" + this.film.imdb;
    for (var i = 0, len = this.film.directors.length; i < len; i++) {
      if (len <= 5) {
        if (i == 0) {
          this.directors += this.film.directors[i]["name"];
        } else {
          this.directors += "/" + this.film.directors[i]["name"];
        }
      } else {
        if (i == 0) {
          this.directors += this.film.directors[i]["name"];
        } else if (i < 5) {
          this.directors += "/" + this.film.directors[i]["name"];
        } else if (i == 5) {
          this.directors += "/更多...";
          break;
        }
      }
    }
    for (var i = 0, len = this.film.writers.length; i < len; i++) {
      if (len <= 5) {
        if (i == 0) {
          this.writers += this.film.writers[i]["name"];
        } else {
          this.writers += "/" + this.film.writers[i]["name"];
        }
      } else {
        if (i == 0) {
          this.writers += this.film.writers[i]["name"];
        } else if (i < 5) {
          this.writers += "/" + this.film.writers[i]["name"];
        } else if (i == 5) {
          this.writers += "/更多...";
          break;
        }
      }
    }
    for (var i = 0, len = this.film.casts.length; i < len; i++) {
      if (len <= 5) {
        if (i == 0) {
          this.casts += this.film.casts[i]["name"];
        } else {
          this.casts += "/" + this.film.casts[i]["name"];
        }
      } else {
        if (i == 0) {
          this.casts += this.film.casts[i]["name"];
        } else if (i < 5) {
          this.casts += "/" + this.film.casts[i]["name"];
        } else if (i == 5) {
          this.casts += "/更多...";
          break;
        }
      }
    }
    for (var i = 0, len = this.film.genres.length; i < len; i++) {
      if (len <= 5) {
        if (i == 0) {
          this.genres += this.film.genres[i];
        } else {
          this.genres += "/" + this.film.genres[i];
        }
      } else {
        if (i == 0) {
          this.genres += this.film.genres[i];
        } else if (i < 5) {
          this.genres += "/" + this.film.genres[i];
        } else if (i == 5) {
          this.genres += "/更多...";
          break;
        }
      }
    }
    for (var i = 0, len = this.film.languages.length; i < len; i++) {
      if (len <= 5) {
        if (i == 0) {
          this.languages += this.film.languages[i];
        } else {
          this.languages += "/" + this.film.languages[i];
        }
      } else {
        if (i == 0) {
          this.languages += this.film.languages[i];
        } else if (i < 5) {
          this.languages += "/" + this.film.languages[i];
        } else if (i == 5) {
          this.languages += "/更多...";
          break;
        }
      }
    }

    this.film.pubdate[0] = this.film.pubdate[0].split(")")[0].split("(")[0];
    for (var i = 0, len = this.film.countries.length; i < len; i++) {
      this.film.countries[i] = this.film.countries[i].replace(")", "");
      this.film.countries[i] = this.film.countries[i].replace("(", "");
    }
    for (var i = 0, len = this.film.countries.length; i < len; i++) {
      if (len <= 5) {
        if (i == 0) {
          this.pubCountries +=
            this.film.pubdate[0] + "(" + this.film.countries[i];
        } else {
          this.pubCountries += "/" + this.film.countries[i];
        }
      } else {
        if (i == 0) {
          this.pubCountries +=
            this.film.pubdate[0] + "(" + this.film.countries[i];
        } else if (i < 5) {
          this.pubCountries += "/" + this.film.countries[i];
        } else if (i == 5) {
          this.pubCountries += "/更多...";
          break;
        }
      }
    }
    this.pubCountries += ")";
    for (var i = 0, len = this.film.aka.length; i < len; i++) {
      if (len <= 5) {
        if (i == 0) {
          this.aka += this.film.aka[i];
        } else {
          this.aka += "/" + this.film.aka[i];
        }
      } else {
        if (i == 0) {
          this.aka += this.film.aka[i];
        } else if (i < 5) {
          this.aka += "/" + this.film.aka[i];
        } else if (i == 5) {
          this.aka += "/更多...";
          break;
        }
      }
    }
    //console.log(this.pubCountries)
  },
  methods: {}
};
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
  margin-right: 2rem;
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
  margin-right: 5rem;
  /* margin-left:2rem */
}
</style>
