<template>
  <div class="f-news-container">
    <div>
      <template v-for="(item, index) in sourceGroupbyDate">
        <v-divider :key="`divider_${index}`"></v-divider>
        <div :key="`title_${index}`" class="date-title">
          {{ fdate(item.key) }}
        </div>
        <template v-for="(jtem, jndex) in item.list">
          <v-divider :key="`divider_${index}_${jndex}`"></v-divider>
          <f-news-preview
            :key="`${index}_${jndex}`"
            :news="jtem"
          ></f-news-preview>
        </template>
      </template>
    </div>
    <div class="more-btn-container">
      <v-btn dark block @click="loadMore">{{
        $t("fNewsContainer.load_more_news")
      }}</v-btn>
    </div>
  </div>
</template>
<script>
import FNewsPreview from "@/components/FNewsPreview";
import helper from "@/assets/utils/helper";
import formatter from "@/assets/utils/formatter";
import { _ } from "vue-underscore";
export default {
  components: {
    FNewsPreview
  },
  props: {
    source: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  data() {
    return {};
  },
  computed: {
    sourceGroupbyDate() {
      const groups = helper.groupby(this.source, "date");
      groups.forEach(g => {
        return {
          key: g.key,
          list: _.sortBy(g.list, "time")
            .reverse()
            .sort((a, b) => (a.image ? -1 : 1))
        };
      });
      return groups;
    }
  },
  methods: {
    fdate: formatter.fdate,
    loadMore() {
      this.$emit("more");
    }
  }
};
</script>
<style scoped>
.f-news-container {
  border: 1px solid rgba(0, 0, 0, 0.12);
  padding: 5px 10px;
}
.date-title {
  font-size: 25px;
  margin-top: 20px;
  color: #f79646;
  font-weight: bold;
}
.more-btn-container {
  margin: 20px 0px;
}
.more-btn-container .v-btn {
  margin: auto;
  background: linear-gradient(45deg, #6540a7, 49%, #dab4ff, 51%, #6540a7);
}
</style>
