<script setup lang="ts">
  import visualizer, {
    type IBot,
    type IEmbed,
  } from './components/visualizer-component.vue';

  const embedData: IEmbed = {
    author: {
      name: 'salut',
      url: 'https://picsum.photos/200/300',
      iconURL: 'https://picsum.photos/200/300',
    },
    footer: {
      text: 'ThunderBot',
      iconURL: 'https://picsum.photos/200/300',
    },
    fields: [
      {
        value: ' sfsf sfs dfsf',
        name: 'testtesttest',
        inline: true,
      },
      {
        value: 'sdfsfsdffffffsgdddssdfddddddsdgsdg',
        name: 'test',
        inline: true,
      },
      {
        value: 'sdfsfsdffffffsgddddddd ddsdgsdg',
        name: 'test',
        inline: true,
      },
      {
        value: 'salut',
        name: 'test',
        inline: true,
      },
      {
        value: 'salut',
        name: 'test',
        inline: true,
      },
      {
        value: 'salut',
        name: 'test',
        inline: true,
      },
      {
        value: 'salut',
        name: 'test',
        inline: true,
      },
      {
        value: 'red',
        name: 'test',
        inline: true,
      },
    ],
    color: 'orange',
    description:
      'Lorem Lorem LoremLoremLoremLorem Lorem Lorem Lorem LoremLorem Lorem Lorem Lorem Lorem  LoremLoremLorem Lorem Lorem Lorem Lorem Lorem  vLorem vvLoremv LoremLorem v v v Lorem vLoremLorem Lorem',
    title: 'Mon super titre',
    url: 'https://picsum.photos/200/300',

    timestamp: true,
  };

  const botData: IBot = {
    name: 'salut',
    iconURL: 'https://picsum.photos/200/300',
  };
</script>
<template>
  <visualizer :embed="embedData" :bot="botData"></visualizer>
</template>

<style scoped></style>
