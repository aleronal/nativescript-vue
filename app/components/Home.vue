<template>
  <Page>
    <ActionBar title="Native Flex" />

    <ListView height="100%" separatorColor="transparent" for="item in flicks" @itemTap="onFlickTap">
      <v-template>
        <GridLayout
          height="200"
          borderRadious="10"
          class="bg-secondary"
          rows="*, auto, auto"
          columns="*"
          margin="5 10"
          padding="0"
        >
          <Image row="0" margin="0" :src="item.image" stretch="aspectFill" />
          <Label
            row="1"
            :text="item.title"
            margin="10 10 0 10"
            fontWeight="700"
            class="text-primary"
            fontSize="18"
          />
          <Label
            row="2"
            margin="0 10 10 10"
            class="text-secondary"
            fontSize="14"
            textWrap="true"
            :text="item.description"
          />
        </GridLayout>

      </v-template>

    </ListView>
  

  </Page>
</template>

<script lang="ts">
import Vue from "nativescript-vue";
import { FlickModel } from "~/models/Flick";
import FlickService from "~/services/FlickService";
import Details from "./Details.vue";

const flickService: FlickService = new FlickService();

export default Vue.extend({
  data() {
    return {
      text: '',
      flicks: flickService.getFlicks(),
    };
  },
  methods:{
    onFlickTap(args:any){
        const flick = args.item as FlickModel;
        this.$navigateTo(Details,{
            transitioniOS: {name: "fade"},
            props: {id: flick.id}
        });
    }
  }
});
</script>