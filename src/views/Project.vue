<template>
  <div style="position:relative;">
    <PageHeader :content="page.fields.name"></PageHeader>
    <v-divider></v-divider>
    <ColumnWrapper>
      <!-- SECTION AND CONTENT FOR PAGE -->
      <div
        v-for="section in page.fields.section"
        :key="section.name"
        class="pa-4 project-content-container"
      >
        <div v-html="section.name"></div>
        <div v-html="section.content"></div>
      </div>
    </ColumnWrapper>

    <v-btn
      fixed
      bottom
      right
      target="_blank"
      v-if="page.fields.github_link"
      :href="page.fields.github_link"
      dark
      fab
      class="ma-2"
    >
      <v-icon large dark>
        mdi-github
      </v-icon>
    </v-btn>
  </div>
</template>

<script>
import { butter } from "@/buttercms";
import PageHeader from "@/components/PageHeader.vue";
//import Subheader from "@/components/Subheader.vue";
import ColumnWrapper from "@/components/ColumnWrapper.vue";

export default {
  components: {
    PageHeader,
    //Subheader,
    ColumnWrapper,
  },
  data() {
    return {
      slug: this.$route.params.project,
      page: {
        fields: {},
      },
    };
  },

  methods: {
    getPage() {
      butter.page
        .retrieve("project", this.slug)
        .then((res) => {
          //console.log(res.data.data);
          this.page = res.data.data;
        })
        .catch((err) => {
          alert("Error fetching content", err);
        });
    },
  },
  beforeRouteEnter(to, from, next) {
    next((vm) => {
      vm.getPage();
    });
  },
};
</script>
