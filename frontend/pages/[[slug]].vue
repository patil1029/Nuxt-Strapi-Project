<template>
  <div>
    <template v-if="checkedIfPagesExist"><h1>Page not found</h1></template>
    <template v-else>
      <div
        v-for="(block, index) in pagesData.pages.data[0].attributes?.blocks"
        :key="'block-' + index"
      >
        <BlockRichText
          v-if="block?.__typename === 'ComponentBlocksRichText'"
          :data="block"
        />
        <BlockSingleImage
          v-if="block?.__typename === 'ComponentBlocksSingleImage'"
          :data="block"
          :class="route.params.slug ? route.params.slug : 'home'"
        />
        <BlockUspOverview
          v-if="block?.__typename === 'ComponentBlocksUsp'"
          :data="block"
        />
        <BlockFoodMakingProcess
          v-if="block?.__typename === 'ComponentBlocksFoodMakingProcess'"
          :data="block"
        />

        <BlockDishesHeroHeader
          v-if="block?.__typename === 'ComponentBlocksDishesServedHero'"
          :data="block"
        />

        <BlockDishesOverview
          v-if="block?.__typename === 'ComponentBlocksDishesServedOverview'"
          :heading="block.heading"
        />

        <BlockOurChefsOverview
          v-if="block?.__typename === 'ComponentBlocksOurChefs'"
          :heading="block.chefHeading"
        />

        <BlockContactHero
          v-if="block?.__typename === 'ComponentBlocksContactHero'"
          :data="block"
        />

        <BlockContactBlock
          v-if="block?.__typename === 'ComponentBlocksContactBlock'"
          :data="block"
        />
      </div>
    </template>
  </div>
</template>

<script lang="ts" setup>
import { getPages } from "../gql/getPages";
import { PageEntityResponseCollection, PageFiltersInput } from "../types";

const route = useRoute();

type resPages = { pages: PageEntityResponseCollection };

const filters: PageFiltersInput = {
  slug: { eq: `${route.params.slug ? route.params.slug : "home"}` },
};

const { data: pagesData, error: pagesError } = await useAsyncQuery<resPages>(
  getPages,
  { filters }
);

const checkedIfPagesExist = computed(
  () => pagesData.value.pages.data && pagesData.value.pages.data.length < 1
);
</script>
