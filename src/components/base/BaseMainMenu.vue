<template>
  <ion-menu side="start" content-id="menu" menu-id="main">
    <ion-header>
      <ion-toolbar class="toolbar">
        <ion-buttons slot="start">
          <ion-button class="close-button" id="main" @click="closeMainMenu">
            <icon-close></icon-close>
          </ion-button>
        </ion-buttons>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <ion-segment class="segment" value="Женщины">
        <ion-segment-button
          class="segment__button"
          v-for="(gender, i) in genders"
          :key="i"
          :tab="gender"
          :value="gender"
        >
          <ion-label class="segment__label">{{ gender }}</ion-label>
        </ion-segment-button>
      </ion-segment>
      <ion-accordion-group :multiple="true">
        <ion-accordion
          class="accordion"
          v-for="accordion in accordions"
          :key="accordion.id"
          :value="accordion.title"
        >
          <ion-item
            class="accordion__item"
            slot="header"
            color="transparent"
            lines="none"
          >
            <ion-label class="accordion__label">{{
              accordion.title
            }}</ion-label>
          </ion-item>
          <ion-list class="accordion__list" slot="content">
            <router-link
              class="accordion__link"
              :to="`#${item}`"
              v-for="(item, idx) in accordion.list"
              :key="idx"
              >{{ item }}</router-link
            >
          </ion-list>
        </ion-accordion>
      </ion-accordion-group>
      <address class="contacts ion-padding">
        <div class="contacts__item">
          <icon-phone />
          <router-link to="#" class="contacts__link"
            >+7(800)-555-35-35</router-link
          >
        </div>
        <div class="contacts__item">
          <icon-location-pin />
          <router-link to="#" class="contacts__link">Местонахождение</router-link>
        </div>
      </address>
      <div class="menu-footer">
        <icon-stick class="menu-footer__stick" />
        <div class="socials">
          <router-link class="socials__link" to="/#"
            ><icon-twitter-dark
          /></router-link>
          <router-link class="socials__link" to="/#"
            ><icon-instagram-dark
          /></router-link>
          <router-link class="socials__link" to="/#"
            ><icon-youtube-dark
          /></router-link>
        </div>
      </div>
    </ion-content>
  </ion-menu>
</template>

<script setup>
import {
  IonHeader,
  IonToolbar,
  IonSegment,
  IonSegmentButton,
  IonButtons,
  IonButton,
  IonMenuToggle,
  IonMenu,
  IonContent,
  IonAccordion,
  IonAccordionGroup,
  IonList,
  IonItem,
  IonLabel,
  menuController,
} from "@ionic/vue";

import {
  IconClose,
  IconPhone,
  IconLocationPin,
  IconTwitterDark,
  IconInstagramDark,
  IconYoutubeDark,
  IconStick,
} from "@/components/icons/index.js";

const genders = ["Женщины", "Мужчины", "Дети"];

const accordions = [
  {
    id: 1,
    title: "Новое",
    list: ["Новое 1", "Новое 2", "Новое 3", "Новое 4", "Новое 5"],
  },
  {
    id: 2,
    title: "Одежда",
    list: [
      "Верхняя",
      "Платья",
      "Блузки/Рубашки",
      "Футболки",
      "Трикотаж",
      "Скит",
      "Брюки",
      "Джинсы",
      "Детская",
    ],
  },
  {
    id: 3,
    title: "Сумки",
    list: [
      "Клачи",
      "Рюкзаки",
      "Сумки Хобо",
      "Портфели",
      "Поясные сумки",
      "Наплечные сумки",
    ],
  },
  {
    id: 4,
    title: "Обувь",
    list: [
      "Кроссовки",
      "Ботинки",
      "Тапочки",
      "Сандали",
      "Спортивная обувь",
      "Ковбойский сапоги",
    ],
  },
  {
    id: 5,
    title: "Аксессуары",
    list: [
      "Цепи",
      "Кольца",
      "Серьги",
      "Пины",
      "Браслеты",
      "Часы",
      "Галстуки",
      "Ремни",
    ],
  },
];

const closeMainMenu = async () => {
  await menuController.close("main");
};
</script>

<style lang="sass" scoped>
ion-header::after
	height: 0

.segment
	--background: #FFFFFF
	margin-bottom: 20px
	&__button
		width: calc(100%/3)
		font-size: 14px
		line-height: 34px
		letter-spacing: 3px
		text-transform: uppercase
		--color: rgba(136, 136, 136, 0.8)
		--color-checked: #212806
		--ripple-color: transparent
		--border-width: 0px
		&::part(native)
			height: 56px
		&::part(indicator)
			position: relative
			padding-bottom: 8.5px
		&::part(indicator)::before
			position: absolute
			content: ''
			bottom: 5px
			background-color: #DD8560
			width: 10px
			height: 10px
			left: calc(50%)
			transform: translate(-50%) rotate(45deg)
		&::part(indicator-background)
			background-color: #DD8560

.ios .segment__button::part(indicator)
	inset: 100% 0px 0px -50%
	transform: translate(0%, -100%)

.accordion
	background: #FFFFFF
	&__item
		--border-width: 0
	&__label
		font-size: 16px
		line-height: 48px
		--color: #333333
	&__list
		background: #FFFFFF
		display: flex
		flex-direction: column
		padding: 0px 32px
	&__link
		font-size: 16px
		line-height: 46px
		text-transform: capitalize
		color: #333333
		text-decoration: none

:deep(.ion-accordion-toggle-icon)
	content: url('/public/assets/icons/arrow-down.svg')

.contacts
	font-style: normal
	&__item
		display: flex
		align-items: center
		& + &
			margin-top: 15px
	&__link
		margin-left: 15px
		font-size: 16px
		line-height: 34px
		color: #555555
		text-decoration: none

.menu-footer
	display: flex
	flex-direction: column
	align-items: center
	&__stick
		margin-top: 10px

.socials
	margin-top: 25px
	width: 150px
	display: flex
	align-items: center
	justify-content: space-between
</style>
