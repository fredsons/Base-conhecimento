<template>
    <div class="articles-by-category">
        <PageTitle icon="fa fa-folder-o"
            :main="category.name" sub="Categoria" />
        <ul>
            <li v-for="article in articles" :key="article.id">
                <ArticleItem :article="article" />
            </li>
        </ul>
        <div class="load-more">
            <button v-if="loadMore"
                class="btn btn-lg  botao"
                @click="getArticles">Carregar Mais Artigos</button>
        </div>
    </div>
</template>

<script>
import { baseApiUrl } from "@/global";
import axios from "axios";
import PageTitle from "../template/PageTitle";
import ArticleItem from "./ArticleItem";

export default {
  name: "ArticlesByCategory",
  components: { PageTitle, ArticleItem },
  data: function() {
    return {
      category: {},
      articles: [],
      page: 1,
      loadMore: true,
    };
  },
  methods: {
    getCategory() {
      const url = `${baseApiUrl}/categories/${this.category.id}`;
      axios(url).then((res) => (this.category = res.data));
    },
    getArticles() {
      const url = `${baseApiUrl}/categories/${this.category.id}/articles?page=${
        this.page
      }`;
      axios(url).then((res) => {
        this.articles = this.articles.concat(res.data);
        this.page++;

        if (res.data.length === 0) this.loadMore = false;
      });
    },
  },
  watch: {
    $route(to) {
      this.category.id = to.params.id;
      this.articles = [];
      this.page = 1;
      this.loadMore = true;

      this.getCategory();
      this.getArticles();
    },
  },
  mounted() {
    this.category.id = this.$route.params.id;
    this.getCategory();
    this.getArticles();
  },
};
</script>

<style>
.articles-by-category ul {
  list-style-type: none;
  padding: 0px;
}

.articles-by-category .load-more {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 25px;
}

.botao {
  border-radius: 4px;
  background-color: lightgray;
  border: none;
  color: #000;
  text-align: center;
  font-size: 20px;
  padding: 16px;
  width: 235px;
  transition: all 0.5s;
  cursor: pointer;
  margin: 15px;
  box-shadow: 0 10px 20px -8px rgba(0, 0, 0, 0.7);
}

.botao {
  cursor: pointer;
  display: inline-block;
  position: relative;
  transition: 0.5s;
}

.botao:after {
  content: "»";
  position: absolute;
  opacity: 0;
  top: 14px;
  right: -20px;
  transition: 0.5s;
}

.botao:hover {
  padding-right: 24px;
  padding-left: 8px;
}

.botao:hover:after {
  opacity: 1;
  right: 10px;
}
</style>
