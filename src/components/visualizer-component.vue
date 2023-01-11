<script setup lang="ts">
  export interface IAuthor {
    name: string;
    url?: string;
    iconURL?: string;
  }

  export interface IField {
    inline?: boolean;
    name: string;
    value: string;
  }

  export interface IFooter {
    text: string;
    iconURL?: string;
  }

  export interface IImage {
    url?: string;
    height?: number;
    width?: number;
  }

  export interface IEmbed {
    author?: IAuthor;
    description?: string;
    color?: string;
    fields?: IField[];
    footer?: IFooter;
    image?: IImage;
    thumbnail?: IImage;
    timestamp?: boolean;
    title?: string;
    url?: string;
  }

  export interface IBot {
    name: string;
    iconURL?: string;
  }

  export interface IProps {
    bot?: IBot;
    embed?: IEmbed;
  }

  function cssProps() {
    if (!props.embed) return;
    return {
      '--bg-color': props.embed.color || '#4f545c',
      '--image-width':
        props.embed.image &&
        'width' in props.embed.image &&
        props.embed.image.width != 0
          ? props.embed.image.width.toString() + 'px'
          : '300px',
      '--image-height':
        props.embed.image &&
        'height' in props.embed.image &&
        props.embed.image.height != 0
          ? props.embed.image.height.toString() + 'px'
          : '300px',
      '--thumbnail-width':
        props.embed.thumbnail &&
        'width' in props.embed.thumbnail &&
        props.embed.thumbnail.width != 0
          ? props.embed.thumbnail.width.toString() + 'px'
          : '80px',
      '--thumbnail-height':
        props.embed.thumbnail &&
        'height' in props.embed.thumbnail &&
        props.embed.thumbnail.height != 0
          ? props.embed.thumbnail.height.toString() + 'px'
          : '80px',
    };
  }

  const props = defineProps<IProps>();
</script>
<template>
  <div class="discord-messages" :style="cssProps()">
    <div class="discord-message">
      <div class="discord-message-content">
        <div
          v-if="props.bot && props.bot.iconURL"
          class="discord-author-avatar"
        >
          <img :src="props.bot.iconURL" alt="" />
        </div>
        <div class="discord-message-body">
          <div v-if="props.bot && props.bot.name">
            <span class="discord-author-info">
              <span class="discord-author-username">{{ props.bot.name }}</span>
              <span class="discord-author-bot-tag">Bot</span>
            </span>
            <span class="discord-message-timestamp">{{
              new Date().toLocaleDateString()
            }}</span>
          </div>
          <div class="discord-embed">
            <div
              class="discord-embed-left-border"
              style="background-color: var(--bg-color)"
            ></div>
            <div class="discord-embed-container">
              <div class="discord-embed-content">
                <div>
                  <div
                    v-if="props.embed && props.embed.author"
                    class="discord-embed-author"
                  >
                    <img
                      v-if="props.embed.author.iconURL"
                      class="discord-embed-author-icon"
                      :src="props.embed.author.iconURL"
                      alt=""
                    />
                    <a
                      v-if="props.embed.author.name && props.embed.author.url"
                      :href="props.embed.author.url"
                      target="_blank"
                      rel="noopener noreferrer"
                    >
                      {{ props.embed.author.name }}
                    </a>
                    <span v-else>
                      {{ props.embed.author.name }}
                    </span>
                  </div>
                  <div
                    v-if="props.embed && props.embed.title"
                    class="discord-embed-title"
                  >
                    <a
                      v-if="props.embed.url"
                      :href="props.embed.url"
                      target="_blank"
                      rel="noopener noreferrer"
                    >
                      {{ props.embed.title }}
                    </a>
                    <span v-else target="_blank" rel="noopener noreferrer">
                      {{ props.embed.title }}
                    </span>
                  </div>
                  <div
                    v-if="props.embed && props.embed.description"
                    class="discord-embed-description"
                  >
                    <!--[-->
                    {{ props.embed.description }}
                    <!--]-->
                  </div>
                  <!--[-->
                  <div
                    v-if="props.embed && props.embed.fields"
                    class="discord-embed-fields"
                  >
                    <!--[-->
                    <div
                      v-for="(field, index) in props.embed.fields"
                      :key="`field-${index}`"
                      class="discord-embed-field"
                      :class="field.inline ? 'discord-embed-field-inline' : ''"
                    >
                      <div class="discord-embed-field-title">
                        {{ field.name }}
                      </div>
                      <!--[-->
                      {{ field.value }}
                      <!--]-->
                    </div>

                    <!--]-->
                  </div>
                  <!--]-->
                  <img
                    v-if="props.embed && props.embed.image"
                    class="discord-embed-image"
                    :src="props.embed.image.url"
                    style="
                      width: var(--image-width);
                      height: var(--image-height);
                    "
                    alt=""
                  />
                </div>
                <img
                  v-if="props.embed && props.embed.thumbnail"
                  class="discord-embed-thumbnail"
                  :src="props.embed.thumbnail.url"
                  style="
                    width: var(--thumbnail-width);
                    height: var(--thumbnail-height);
                  "
                  alt=""
                />
              </div>
              <div class="discord-embed-footer">
                <img
                  v-if="
                    props.embed &&
                    props.embed.footer &&
                    props.embed.footer.iconURL
                  "
                  class="discord-embed-footer-icon"
                  :src="props.embed.footer.iconURL"
                  alt=""
                />
                <span>
                  <!--[-->
                  <span
                    v-if="
                      props.embed &&
                      props.embed.footer &&
                      props.embed.footer.text
                    "
                    >{{ props.embed.footer.text }}</span
                  >
                  <!--]-->
                  <span
                    v-if="
                      props.embed &&
                      props.embed.footer &&
                      props.embed.footer.text
                    "
                    class="discord-embed-footer-separator"
                    >•</span
                  >
                  <span v-if="props.embed && props.embed.timestamp">
                    {{ new Date().toLocaleDateString() }}</span
                  >
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .discord-messages a {
    text-decoration: none !important;
    grid-column: 1/2;
  }
  .discord-messages a:hover {
    text-decoration: underline !important;
  }
  .discord-messages {
    color: #fff;
    background-color: #2c2f33;
    font-size: 16px;
    font-family: Roboto, sans-serif;
    line-height: 170%;
    border: 1px solid rgba(255, 255, 255, 0.05);
  }
  .discord-messages {
    border-radius: 0.375rem;
  }
  .discord-message {
    color: #dcddde;
    display: flex;
    flex-direction: column;
    font-size: 0.9em;
    margin: 1em 0;
    padding: 0.25em 1em 0;
  }

  .discord-message .discord-message-content {
    display: flex;
    width: 100%;
    line-height: 160%;
    font-weight: 400;
    overflow-wrap: anywhere;
  }
  .discord-message .discord-author-avatar {
    margin-top: 1px;
    margin-right: 16px;
    min-width: 40px;
  }

  .discord-message .discord-message-body {
    position: relative;
    width: 100%;
  }

  .discord-message .discord-author-avatar img {
    width: 40px;
    height: 40px;
    border-radius: 50%;
  }

  .discord-message .discord-author-info {
    color: #fff;
    display: inline-flex;
    align-items: center;
    font-size: 15px;
  }
  .discord-message .discord-author-info .discord-author-username {
    font-size: 1.1em;
    font-weight: 500;
    letter-spacing: 0.5px;
  }
  .discord-message .discord-author-info .discord-author-bot-tag {
    background-color: #5865f2;
    font-size: 0.65em;
    margin-left: 5px;
    padding: 3px 4px;
    border-radius: 3px;
    line-height: 100%;
    text-transform: uppercase;
  }

  .discord-message .discord-message-content .discord-message-timestamp {
    color: #72767d;
    font-size: 12px;
    margin-left: 3px;
  }

  .discord-embed {
    color: #dcddde;
    display: flex;
    margin-top: 8px;
    margin-bottom: 8px;
    font-size: 13px;
    line-height: 150%;
  }
  .discord-light-theme .discord-embed {
    color: #2e3338;
  }
  .discord-embed .discord-embed-left-border {
    background-color: #202225;
    flex-shrink: 0;
    width: 4px;
    border-radius: 4px 0 0 4px;
  }
  .discord-light-theme .discord-embed .discord-embed-left-border {
    background-color: #e3e5e8;
  }
  .discord-embed .discord-embed-container {
    background-color: #2f3136;
    display: flex;
    flex-direction: column;
    max-width: 520px;
    padding: 8px 16px 16px;
    border: 1px solid rgba(46, 48, 54, 0.6);
    border-radius: 0 4px 4px 0;
  }
  .discord-light-theme .discord-embed .discord-embed-container {
    background-color: #f9f9f94d;
    border-color: #cdcdcd4d;
  }
  .discord-embed .discord-embed-content {
    display: flex;
  }
  .discord-embed .discord-embed-content .discord-embed-author {
    color: #fff;
    display: flex;
    align-items: center;
    font-weight: 500;
    margin-top: 8px;
  }
  .discord-light-theme
    .discord-embed
    .discord-embed-content
    .discord-embed-author,
  .discord-light-theme
    .discord-embed
    .discord-embed-content
    .discord-embed-author
    a {
    color: #4f545c;
  }
  .discord-embed .discord-embed-content .discord-embed-author a {
    color: #fff;
    font-weight: 500;
  }
  .discord-embed
    .discord-embed-content
    .discord-embed-author
    .discord-embed-author-icon {
    width: 24px;
    height: 24px;
    margin-right: 8px;
    border-radius: 50%;
  }
  .discord-embed .discord-embed-content .discord-embed-title {
    color: #fff;
    font-size: 16px;
    font-weight: 600;
    margin-top: 8px;
  }
  .discord-embed .discord-embed-content .discord-embed-title a {
    color: #00b0f4;
    font-weight: 600;
    text-decoration: none;
  }

  .discord-embed .discord-embed-content .discord-embed-description {
    margin-top: 8px;
  }
  .discord-embed .discord-embed-content .discord-embed-image {
    max-width: 100%;
    margin-top: 16px;
    border-radius: 4px;
  }
  .discord-embed .discord-embed-content .discord-embed-thumbnail {
    max-width: 80px;
    max-height: 80px;
    margin-left: 16px;
    margin-top: 8px;
    border-radius: 4px;
    -o-object-fit: contain;
    object-fit: contain;
    -o-object-position: top center;
    object-position: top center;
  }
  .discord-embed .discord-embed-footer {
    color: #72767d;
    display: flex;
    align-items: center;
    font-size: 0.85em;
    margin-top: 8px;
  }
  .discord-embed .discord-embed-footer .discord-embed-footer-icon {
    flex-shrink: 0;
    width: 20px;
    height: 20px;
    margin-right: 8px;
    border-radius: 50%;
  }
  .discord-embed .discord-embed-footer .discord-embed-footer-separator {
    color: #3b3c42;
    font-weight: 700;
    margin: 0 4px;
  }
  .discord-light-theme
    .discord-embed
    .discord-embed-footer
    .discord-embed-footer-separator {
    color: #e4e4e4;
  }
  .discord-embed .discord-embed-field {
    min-width: 100%;
    margin-top: 5px;
  }
  .discord-embed .discord-embed-field.discord-embed-field-inline {
    flex-grow: 1;
    flex-basis: auto;
    min-width: 100px;
  }
  .discord-embed .discord-embed-field .discord-embed-field-title {
    color: #72767d;
    font-weight: 500;
    margin-bottom: 2px;
  }
  .discord-light-theme
    .discord-embed
    .discord-embed-field
    .discord-embed-field-title {
    color: #747f8d;
  }
  .discord-embed .discord-embed-fields {
    display: flex;
    flex-wrap: wrap;
    line-gap-override: 50;
    margin-top: 8px;
  }
</style>
