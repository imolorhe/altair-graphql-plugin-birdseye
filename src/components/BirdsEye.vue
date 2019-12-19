<template>
  <div />
</template>

<script lang="ts">
const GraphqlBirdseyeCore = require('graphql-birdseye-core');
// import {
//   GraphqlBirdseye,
//   IntrospectionDataStructure,
// } from "graphql-birdseye-core";
import Vue from 'vue';
import { buildSchema } from 'graphql';

const birdseye = new GraphqlBirdseyeCore.GraphqlBirdseye();

const sdl = `
type A implements ParentInterface {
  name: String
  number: Int
  otherName: String
}

type B implements ParentInterface {
  name: String
  number: Int
  yetAnotherName: String
}

interface ParentInterface {
  name: String
  number: Int
}

type Query {
  field: ParentInterface
}
`;

export default Vue.extend({
  name: 'BirdsEye',
  props: {
    props: {
      type: Object,
      default: () => ({}),
    },
  },
  mounted() {
    const dataStructure = new GraphqlBirdseyeCore.SchemaDataStructure(
      buildSchema(sdl)
    );
    this.$nextTick(() => {
      // eslint-disable-next-line
      console.log('birdseye', this.$el);
      birdseye.init(this.$el, {}, dataStructure);

      // this.props contains `props` as passed from Altair
      // eslint-disable-next-line
      console.log('BIRDSEYE', this.props);

      // You can access Altair lifecycle methods using this.props.ctx.on('event', handler)
      // Check the plugin-prop-factory.ts in altair for now to know all available props, based on if it is app level, or window level
      // eslint-disable-next-line
      this.props.ctx.on('app-ready', () => console.log('BIRDSEYE app-ready'));
    });
  },
});
</script>
