<template>
  <div v-if="tags" class="tags-wrapper">
    <q-badge
      v-for="tag in tags"
      class="tag q-px-sm q-py-xs"
      :class="{ dark: $q.dark.isActive }"
      :key="tag"
      @click="searchByTag(tag)"
      rounded
      :color="$q.dark.isActive ? 'grey-3' : 'grey-9'"
      outline
      :text-color="$q.dark.isActive ? 'grey-3' : 'grey-9'"
      size="2rem"
      :label="tag"
    />
  </div>
</template>

<script lang="ts" setup>
import { RouteNames } from 'src/router/routes';
import { toRefs } from 'vue';
import { useRouter } from 'vue-router';

const props = defineProps<{
  tags?: string[];
}>();

const { tags } = toRefs(props);

const router = useRouter();
const searchByTag = (tag: string) => {
  router.push({
    name: RouteNames.NoteList,
    query: {
      q: tag,
    },
  });
};
</script>

<style lang="scss">
.tags-wrapper {
  padding: 0 0.5rem;
}
.tag {
  cursor: pointer;
  &:not(:first-child) {
    margin-left: 0.5rem;
  }

  &:hover {
    background-color: $grey-9;
    color: $grey-3 !important;
  }

  &.dark:hover {
    background-color: $grey-3;
    color: $grey-9 !important;
  }
}
</style>
