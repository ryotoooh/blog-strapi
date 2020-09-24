<template>
  <div>
    <div class="uk-section">
      <div class="uk-container uk-container-large">
        <h1>{{ categories[0].name }}</h1>

        <ArticlesList :articles="categories[0].articles || []"></ArticlesList>
      </div>
    </div>
  </div>
</template>

<script>
import ArticlesList from "../containers/ArticlesList";
import gql from "graphql-tag";
export default {
  data() {
    return {
      categories: [[]],
      routeParam: this.$route.params.name
    };
  },
  components: {
    ArticlesList
  },
  apollo: {
    categories: {
      query: gql`
        query Categories($name: String!) {
          categories(where:{name: $name}) {
            name
            articles {
              id
              title
              content
              image {
                url
              }
              category {
                id
                name
              }
            }
          }
        }
      `,
      variables() {
        return { name: this.routeParam };
      }
    }
  }
};
</script>