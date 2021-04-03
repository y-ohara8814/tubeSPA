<template>
  <div>
    <h1>YoutubeList</h1>
    <v-row>
      <v-col cols="6">
        <v-text-field
          label="動画のタイトルを検索"
          v-model="keyword"
        ></v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="3">
        <v-btn color="error" @click="search(keyword)">検索する</v-btn>
      </v-col>
      <v-col cols="3">
        <v-btn color="secondary" to="/">一覧にもどる</v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col
        class="my-2"
        cols="12"
        md="6"
        v-for="(movie, index) in searchResults"
        :key="movie.index"
      >
        <v-card class="mx-auto">
          <v-row>
            <v-col cols="4">
              <v-img :src="movie.img"></v-img>
            </v-col>
            <v-col cols="8">
              <v-card-title>{{ movie.title }}</v-card-title>
              {{ movie.description }}
              <v-spacer></v-spacer>
              <v-card-actions>
                <v-btn fab dark color="indigo" @click="addBookList(index)">
                  <v-icon dark>mdi-plus</v-icon>
                </v-btn>
              </v-card-actions>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: "TubeSearch",
  data() {
    return {
      keyword: "",
      searchResults: [],
    };
  },
  methods: {
    // クエリストリングを作成
    // async search(keyword) {
    //   this.searchResults = [];
    //   const baseURL = "https://www.googleapis.com/youtube/v3/search";
    //   const params = {
    //     type: "video",
    //     part: "snippet",
    //     q: `intitle:${keyword}`,
    //     key: "AIzaSyCycq8YPFjdLhpaR2Aia6VZ7ECJmsS16lA",
    //     maxResults: 40,
    //   };
    //   const queryParams = new URLSearchParams(params);

    //   // fetchで、APIのレスポンス(JSON)を取得
    //   const response = await fetch(baseURL + queryParams).then((response) =>
    //     // response.json()
    //     console.log(response)
    //   );

    //   // JSONの中の、必要な情報をsearchResults配列にpushで追加
    //   for (let movie of response.items) {
    //     let title = movie.snippet.title;
    //     let img = movie.snippet.thumbnails.high;
    //     let description = movie.snippet.description;
    //     this.searchResults.push({
    //       title: title ? title : "タイトルなし",
    //       image: img ? img.thumbnail : "NO IMAGE",
    //       description: description ? description.slice(0, 40) : "",
    //     });
    //   }
    // },
    search(keyword) {
      this.searchResults = [];
      const baseURL = "https://www.googleapis.com/youtube/v3/search";
      const params = {
        type: "video",
        part: "snippet",
        q: `intitle:${keyword}`,
        key: "AIzaSyCycq8YPFjdLhpaR2Aia6VZ7ECJmsS16lA",
        maxResults: 40,
      };
      axios.get(this.baseURL, +params).then((response) => {
        // this.searchResults = response;
        console.log(response);
      });
    },
  },
};
</script>
