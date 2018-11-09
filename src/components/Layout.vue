<template lang="pug">
  div(class="grid")
    header(class="header")
      div(class="menu")
        img(:src="`${baseUrl}menu.svg`" @click.stop="open")
      span(class="logo") LOGO
      div(class="close" :class="{ opened : isOpened }")
        img(:src="`${baseUrl}close.svg`" @click.stop="close")

      nav(class="menu-lateral" :class="{ opened : isOpened }")
        h2(class="title") LOGO
        ul(class="list")
          li(v-for="(link, index) in links" :key="index" class="link") {{ link }}

    main(class="content")
      div(v-for="(item, index) in items" :key="index" class="item" :class="{ opened : isOpened }") {{ item }}

    footer(class="footer")
      span Footer

</template>

<script>
export default {
  name: 'Layout',
  data () {
    return {
      baseUrl: process.env.BASE_URL,
      isOpened: false,
      items: ['A', 'B', 'C', 'D', 'E', 'F'],
      links: ['About', 'Clients', 'Works', 'About']
    }
  },
  methods: {
    open () {
      this.isOpened = true
    },
    close () {
      this.isOpened = false
    },
    // Comportamineto necesario en el caso de tener abierto el menu lateral
    checkIfItsMenuLateralOpened () {
      if (window.innerWidth > 768) {
        this.isOpened = false
      }
    }
  },
  created () {
    window.addEventListener('resize', this.checkIfItsMenuLateralOpened)
  }
}
</script>

<style lang="scss" scoped>
 @import '../scss/main.scss';

  .grid {
    display: grid;
    grid-template-rows: 48px auto 120px;
    min-height: 100vh;

    @include if-tablet-portrait {
      grid-template-rows: 96px auto 200px;
    }

    .header {
      display: grid;
      grid: auto / repeat(3, 1fr);
      background: $header;
      align-items: center;
      padding: 0 18px;
      height: 48px;

      @include if-tablet-portrait {
        grid: auto / repeat(2, 1fr);
        padding: 0 48px;
        height: 96px;
      }

      .menu {

        img {
          cursor: pointer;
        }

         @include if-tablet-portrait {
          display: none;
        }
      }

      .logo {
        justify-self: center;
        letter-spacing: 0.225rem;

        @include if-tablet-portrait {
          justify-self: start;
        }
      }

      .close {
        opacity: 0;
        justify-self: end;
        @include transition($attr: opacity);

        @include if-tablet-portrait {
          display: none;
        }

        &.opened {
          opacity: 1;
        }
      }

      .menu-lateral {
        width: 270px;
        background: $lateral-menu;
        min-height: 100vh;
        position: absolute;
        z-index: 1;
        left: -270px;
        top: 0;
        box-shadow: 2px 0 2px 0 rgba(0,0,0,0.30);
        color: $lateral-menu-font-color;
        font-weight: 400;

        @include transition($attr: left);

        @include if-tablet-portrait {
          width: 100%;
          position: static;
          left: 0;
          min-height: 96px;
          box-shadow: none;
        }

        &.opened {
          left: 0;
        }

        .title {
          text-align: center;
          margin-top: 48px;
          font-weight: 400;

          @include if-tablet-portrait {
            display: none;
          }
        }

        .list {
          list-style-type: none;
          margin: 0;
          padding-left: 30px;

          @include if-tablet-portrait {
            display: grid;
            grid: 96px / repeat(4, 1fr);
            align-items: center;
            padding-left: 0;
            color: $white-01;
            background: $gray-01;
          }

          .link {
            margin-bottom: 29px;

            @include if-tablet-portrait {
              text-align: center;
              margin-bottom: 0;
              margin: 0 20px;
            }
          }
        }
      }
    }

    .footer {
      display: grid;
      grid: auto / auto;
      background:  $footer;
      align-items: center;
      justify-content: center;
      letter-spacing: 0.125rem;
      position: fixed;
      bottom: 0;
      width: 100%;
      height: 120px;

      @include if-tablet-portrait {
        height: 200px;
      }
    }

    .content {
      display: grid;
      grid: repeat(6, 1fr);
      grid-gap: 8px;
      margin: 16px 10px;
      @include transition;
      overflow: hidden;

      @include if-tablet-portrait {
        grid: repeat(2, 1fr) / repeat(3, 1fr);
      }

      .item {
        display: grid;
        align-items: end;
        height: 120px;
        background: $items-background-color;
        padding-left: 8px;
        font-size: 2.5rem;
        border-radius: 4px;
        @include transition;

        @include if-tablet-portrait {
          height: auto;
        }

        &.opened {
            transform: translate3d(270px, 0 , 0);
            @include transition;
          }
      }
    }
  }

</style>
