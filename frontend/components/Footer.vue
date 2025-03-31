<template>
  <div class="footer-wrapper">
    <div class="footer container">
      <div
        class="contact-info-wrapper"
        v-if="footerData?.contactInfo?.data?.attributes"
      >
        <h3>{{ footerData?.contactInfo?.data?.attributes.heading }}</h3>
        <ContactInfo
          v-for="(contactData, index) in footerData?.contactInfo?.data
            ?.attributes.contactInfo"
          :contactData="contactData"
          :key="index"
        />
      </div>

      <div class="navlinks">
        <h3>All Pages</h3>
        <ul>
          <li
            v-for="(item, index) in footerData?.navigation?.data?.attributes
              ?.navItems"
            :key="index"
          >
            <NavSubItem
              v-if="item"
              :name="item.title"
              :url="item.url"
            ></NavSubItem>
          </li>
        </ul>
      </div>

      <div v-if="footerData?.openingHour?.data?.attributes" class="openingtime">
        <h3>{{ footerData?.openingHour?.data.attributes.heading }}</h3>
        <p>{{ footerData?.openingHour.data.attributes.workingDays }}</p>
        <p>
          {{
            footerData?.openingHour.data.attributes.openTimings?.openHour.slice(
              0,
              5
            )
          }}
          -
          {{
            footerData?.openingHour.data.attributes.openTimings?.closingHour.slice(
              0,
              5
            )
          }}
        </p>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import type { GetFooterQuery } from "../types";

const props = defineProps({
  footerData: {
    type: Object as PropType<GetFooterQuery>,
  },
});
</script>
