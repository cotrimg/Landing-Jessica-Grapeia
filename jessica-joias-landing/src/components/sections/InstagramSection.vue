<script setup>
import {
  onBeforeUnmount,
  onMounted,
  ref,
} from 'vue'

import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

import {
  instagramPosts,
  instagramProfile,
} from '../../data/instagramPosts'

gsap.registerPlugin(ScrollTrigger)

const sectionElement = ref(null)

let animationContext

onMounted(() => {
  const reduceMotion = window.matchMedia(
    '(prefers-reduced-motion: reduce)'
  ).matches

  if (reduceMotion) {
    return
  }

  animationContext = gsap.context(() => {
    gsap.from('.instagram__eyebrow', {
      opacity: 0,
      y: 24,
      duration: 0.7,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.instagram__header',
        start: 'top 84%',
        once: true,
      },
    })

    gsap.from('.instagram__title-line', {
      opacity: 0,
      yPercent: 110,
      rotate: 2,
      duration: 1,
      stagger: 0.12,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.instagram__title',
        start: 'top 85%',
        once: true,
      },
    })

    gsap.from('.instagram__introduction', {
      opacity: 0,
      y: 35,
      duration: 0.8,
      delay: 0.15,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.instagram__header',
        start: 'top 84%',
        once: true,
      },
    })

    gsap.from('.instagram-card', {
      opacity: 0,
      y: 70,
      scale: 0.95,
      duration: 0.9,
      stagger: 0.1,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.instagram__grid',
        start: 'top 80%',
        once: true,
      },
    })

    gsap.from('.instagram__profile', {
      opacity: 0,
      y: 35,
      duration: 0.8,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.instagram__profile',
        start: 'top 88%',
        once: true,
      },
    })

    gsap.to('.instagram__background-word', {
      xPercent: -14,
      ease: 'none',
      scrollTrigger: {
        trigger: sectionElement.value,
        start: 'top bottom',
        end: 'bottom top',
        scrub: 1,
      },
    })
  }, sectionElement.value)
})

onBeforeUnmount(() => {
  animationContext?.revert()
})
</script>

<template>
  <section
    id="instagram"
    ref="sectionElement"
    class="instagram"
    aria-labelledby="instagram-title"
  >
    <div
      class="instagram__background-word"
      aria-hidden="true"
    >
      INSTAGRAM
    </div>

    <div class="instagram__container">
      <header class="instagram__header">
        <div class="instagram__heading">
          <span class="instagram__eyebrow">
            Acompanhe a marca
          </span>

          <h2
            id="instagram-title"
            class="instagram__title"
          >
            <span class="instagram__title-mask">
              <span class="instagram__title-line">
                Inspirações,
              </span>
            </span>

            <span class="instagram__title-mask">
              <span
                class="
                  instagram__title-line
                  instagram__title-line--accent
                "
              >
                detalhes e novidades.
              </span>
            </span>
          </h2>
        </div>

        <div class="instagram__introduction">
          <p>
            Acompanhe as novidades, descubra novas peças
            e veja de perto os detalhes das coleções da
            Jessica Grapeia Joias.
          </p>

          <a
            :href="instagramProfile.url"
            target="_blank"
            rel="noopener noreferrer"
            class="instagram__header-link"
          >
            Seguir no Instagram

            <span aria-hidden="true">↗</span>
          </a>
        </div>
      </header>

      <div class="instagram__grid">
        <a
          v-for="post in instagramPosts"
          :key="post.id"
          :href="post.link"
          target="_blank"
          rel="noopener noreferrer"
          class="instagram-card"
          :class="{
            'instagram-card--large':
              post.size === 'large',

            'instagram-card--wide':
              post.size === 'wide',

            'instagram-card--portrait':
              post.size === 'portrait',

            'instagram-card--brand':
              post.type === 'brand',
          }"
          :aria-label="`${post.alt}. Abrir Instagram.`"
        >
          <img
            :src="post.image"
            :alt="post.alt"
            :style="{
              objectPosition: post.position,
            }"
            class="instagram-card__image"
            loading="lazy"
            width="800"
            height="1000"
          >

          <div class="instagram-card__shade"></div>

          <div class="instagram-card__content">
            <span
              class="instagram-card__icon"
              aria-hidden="true"
            >
              <svg
                viewBox="0 0 24 24"
                role="presentation"
              >
                <rect
                  x="3"
                  y="3"
                  width="18"
                  height="18"
                  rx="5"
                />

                <circle
                  cx="12"
                  cy="12"
                  r="4"
                />

                <circle
                  cx="17.5"
                  cy="6.5"
                  r="1"
                  class="instagram-card__icon-dot"
                />
              </svg>
            </span>

            <span class="instagram-card__action">
              Ver publicação
            </span>
          </div>

          <span
            v-if="post.type !== 'brand'"
            class="instagram-card__number"
          >
            {{ String(post.id).padStart(2, '0') }}
          </span>
        </a>
      </div>

      <div class="instagram__profile">
        <div class="instagram__profile-identity">
          <div
            class="instagram__avatar"
            aria-hidden="true"
          >
            JG
          </div>

          <div>
            <span>Instagram</span>

            <strong>
              {{ instagramProfile.username }}
            </strong>
          </div>
        </div>

        <p>
          Novas peças, inspirações e detalhes especiais
          publicados no perfil da marca.
        </p>

        <a
          :href="instagramProfile.url"
          target="_blank"
          rel="noopener noreferrer"
          class="instagram__button"
        >
          Visitar perfil

          <span aria-hidden="true">↗</span>
        </a>
      </div>
    </div>
  </section>
</template>

<style scoped>
.instagram {
  position: relative;
  isolation: isolate;
  overflow: hidden;

  padding:
    clamp(105px, 13vw, 190px)
    32px;

  background:
    radial-gradient(
      circle at 83% 16%,
      rgba(246, 88, 168, 0.13),
      transparent 27%
    ),
    linear-gradient(
      180deg,
      #ffffff,
      #fff8fb
    );
}

.instagram__container {
  position: relative;
  z-index: 2;

  width: min(100%, 1320px);
  margin-inline: auto;
}

.instagram__header {
  display: grid;
  grid-template-columns:
    minmax(0, 1.25fr)
    minmax(290px, 0.75fr);
  align-items: end;
  gap: clamp(45px, 8vw, 115px);

  margin-bottom: clamp(60px, 9vw, 115px);
}

.instagram__eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 12px;

  margin-bottom: 19px;

  color: var(--color-pink-dark);
  font-size: 0.73rem;
  font-weight: 800;
  letter-spacing: 0.21em;
  text-transform: uppercase;
}

.instagram__eyebrow::before {
  content: '';

  width: 38px;
  height: 1px;

  background-color: currentColor;
}

.instagram__title {
  max-width: 820px;

  font-family: Georgia, 'Times New Roman', serif;
  font-size: clamp(3.3rem, 6.8vw, 7rem);
  font-weight: 400;
  line-height: 0.88;
  letter-spacing: -0.055em;
}

.instagram__title-mask {
  display: block;
  overflow: hidden;
  padding-bottom: 0.08em;
}

.instagram__title-line {
  display: block;
  transform-origin: left center;
}

.instagram__title-line--accent {
  color: var(--color-pink-dark);
  font-style: italic;
}

.instagram__introduction {
  max-width: 430px;
  padding-bottom: 8px;
}

.instagram__introduction p {
  color: var(--color-muted);
  font-size: 1rem;
  line-height: 1.75;
}

.instagram__header-link {
  display: inline-flex;
  align-items: center;
  gap: 14px;

  margin-top: 26px;
  padding-bottom: 7px;

  border-bottom:
    1px solid rgba(40, 34, 40, 0.25);

  color: var(--color-text);
  font-size: 0.76rem;
  font-weight: 800;
  letter-spacing: 0.08em;
  text-decoration: none;
  text-transform: uppercase;

  transition:
    color 200ms ease,
    border-color 200ms ease,
    gap 200ms ease;
}

.instagram__header-link:hover {
  gap: 20px;
  color: var(--color-pink-dark);
  border-color: var(--color-pink-dark);
}

.instagram__grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 250px;
  gap: 18px;
}

.instagram-card {
  position: relative;
  overflow: hidden;

  min-height: 250px;
  border-radius: 25px;

  color: var(--color-white);
  background-color: var(--color-pink-light);

  box-shadow:
    0 22px 55px rgba(104, 36, 73, 0.1);

  text-decoration: none;
  isolation: isolate;
}

.instagram-card--large {
  grid-column: span 2;
  grid-row: span 2;
}

.instagram-card--wide {
  grid-column: span 2;
}

.instagram-card--portrait {
  grid-row: span 2;
}

/*
  Tratamento especial da fotografia institucional.
  O raio superior foi reduzido para preservar melhor
  os cantos e o enquadramento da fotografia.
*/
.instagram-card--brand {
  min-height: 518px;
  border-radius: 80px 80px 25px 25px;
  background-color: #f7e9f0;
}

.instagram-card__image {
  width: 100%;
  height: 100%;

  object-fit: cover;
  object-position: center;

  transition:
    transform 900ms
      cubic-bezier(0.16, 1, 0.3, 1),
    filter 500ms ease;
}

.instagram-card--brand .instagram-card__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center center;
}

.instagram-card__shade {
  position: absolute;
  z-index: 1;
  inset: 0;

  background:
    linear-gradient(
      to top,
      rgba(33, 15, 25, 0.72),
      rgba(33, 15, 25, 0.02) 58%
    );

  opacity: 0;

  transition: opacity 400ms ease;
}

.instagram-card--brand .instagram-card__shade {
  background:
    linear-gradient(
      to top,
      rgba(33, 15, 25, 0.48),
      transparent 48%
    );
}

.instagram-card__content {
  position: absolute;
  z-index: 3;
  right: 22px;
  bottom: 20px;
  left: 22px;

  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;

  opacity: 0;
  transform: translateY(16px);

  transition:
    opacity 400ms ease,
    transform 400ms ease;
}

.instagram-card__icon {
  width: 42px;
  height: 42px;

  display: grid;
  place-items: center;

  border: 1px solid rgba(255, 255, 255, 0.6);
  border-radius: 50%;

  background-color: rgba(255, 255, 255, 0.16);
  backdrop-filter: blur(10px);
}

.instagram-card__icon svg {
  width: 21px;
  height: 21px;

  fill: none;
  stroke: currentColor;
  stroke-width: 1.7;
}

.instagram-card__icon-dot {
  fill: currentColor;
  stroke: none;
}

.instagram-card__action {
  font-size: 0.68rem;
  font-weight: 800;
  letter-spacing: 0.14em;
  text-transform: uppercase;
}

.instagram-card__number {
  position: absolute;
  z-index: 3;
  top: 20px;
  left: 21px;

  width: 42px;
  height: 42px;

  display: grid;
  place-items: center;

  border: 1px solid rgba(255, 255, 255, 0.55);
  border-radius: 50%;

  color: var(--color-white);
  background-color: rgba(25, 12, 20, 0.13);
  backdrop-filter: blur(10px);

  font-size: 0.65rem;
  font-weight: 800;
  letter-spacing: 0.08em;
}

.instagram-card:hover .instagram-card__image {
  transform: scale(1.08);
  filter: saturate(1.08);
}

/*
  Define um zoom menor na foto institucional para
  evitar que o hover volte a cortar a fotografia.
*/
.instagram-card--brand:hover .instagram-card__image {
  transform: scale(1.025);
}

.instagram-card:hover .instagram-card__shade {
  opacity: 1;
}

.instagram-card:hover .instagram-card__content {
  opacity: 1;
  transform: translateY(0);
}

.instagram-card:focus-visible {
  outline: 3px solid var(--color-gold);
  outline-offset: 6px;
}

.instagram__profile {
  display: grid;
  grid-template-columns:
    auto
    minmax(220px, 1fr)
    auto;
  align-items: center;
  gap: clamp(25px, 5vw, 70px);

  margin-top: 55px;
  padding:
    26px
    clamp(25px, 4vw, 48px);

  border: 1px solid rgba(200, 47, 121, 0.13);
  border-radius: 30px;

  background-color: rgba(255, 255, 255, 0.72);

  box-shadow:
    0 24px 60px rgba(104, 36, 73, 0.07);

  backdrop-filter: blur(18px);
}

.instagram__profile-identity {
  display: flex;
  align-items: center;
  gap: 17px;
}

.instagram__avatar {
  flex: 0 0 auto;

  width: 62px;
  height: 62px;

  display: grid;
  place-items: center;

  border: 4px solid var(--color-white);
  border-radius: 50%;

  color: var(--color-white);

  background:
    linear-gradient(
      135deg,
      #f7a6ca,
      var(--color-pink-dark),
      #b99052
    );

  box-shadow:
    0 10px 25px rgba(200, 47, 121, 0.2);

  font-family: Georgia, 'Times New Roman', serif;
  font-size: 1rem;
}

.instagram__profile-identity div:last-child {
  display: grid;
  gap: 4px;
}

.instagram__profile-identity span {
  color: var(--color-muted);
  font-size: 0.65rem;
  font-weight: 800;
  letter-spacing: 0.16em;
  text-transform: uppercase;
}

.instagram__profile-identity strong {
  color: var(--color-text);
  font-size: 0.92rem;
}

.instagram__profile > p {
  max-width: 480px;

  color: var(--color-muted);
  font-size: 0.86rem;
  line-height: 1.6;
}

.instagram__button {
  min-height: 52px;
  padding-inline: 23px;

  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 13px;

  border-radius: 999px;

  color: var(--color-white);
  background-color: var(--color-pink-dark);

  font-size: 0.78rem;
  font-weight: 800;
  text-decoration: none;

  transition:
    transform 200ms ease,
    background-color 200ms ease,
    box-shadow 200ms ease;
}

.instagram__button:hover {
  transform: translateY(-3px);
  background-color: var(--color-pink);

  box-shadow:
    0 17px 35px rgba(200, 47, 121, 0.24);
}

.instagram__button:focus-visible,
.instagram__header-link:focus-visible {
  outline: 3px solid var(--color-gold);
  outline-offset: 4px;
}

.instagram__background-word {
  position: absolute;
  z-index: -1;
  right: -6%;
  bottom: 1%;

  color: rgba(200, 47, 121, 0.026);

  font-family: Georgia, 'Times New Roman', serif;
  font-size: clamp(8rem, 20vw, 22rem);
  line-height: 0.7;
  letter-spacing: -0.08em;

  white-space: nowrap;
  pointer-events: none;
  user-select: none;
  will-change: transform;
}

@media (max-width: 1000px) {
  .instagram__header {
    grid-template-columns: 1fr;
    gap: 30px;
  }

  .instagram__introduction {
    max-width: 590px;
  }

  .instagram__grid {
    grid-template-columns: repeat(2, 1fr);
    grid-auto-rows: 275px;
  }

  .instagram-card--large {
    grid-column: span 2;
  }

  .instagram-card--wide {
    grid-column: span 2;
  }

  .instagram-card--portrait {
    grid-row: span 2;
  }

  .instagram-card--brand {
    min-height: 568px;
  }

  .instagram__profile {
    grid-template-columns: 1fr auto;
  }

  .instagram__profile > p {
    grid-column: 1 / -1;
    grid-row: 2;
  }
}

@media (max-width: 620px) {
  .instagram {
    padding:
      90px
      20px
      105px;
  }

  .instagram__title {
    font-size: clamp(3rem, 16vw, 4.9rem);
  }

  .instagram__grid {
    grid-template-columns: repeat(2, 1fr);
    grid-auto-rows: 190px;
    gap: 11px;
  }

  .instagram-card {
    min-height: 190px;
    border-radius: 18px;
  }

  .instagram-card--large {
    grid-column: span 2;
    grid-row: span 2;
  }

  .instagram-card--wide {
    grid-column: span 2;
  }

  .instagram-card--portrait {
    grid-column: span 2;
    grid-row: span 3;
  }

  .instagram-card--brand {
    min-height: 590px;
    border-radius: 55px 55px 20px 20px;
  }

  .instagram-card--brand .instagram-card__image {
    object-fit: contain;
    object-position: center;
  }

  .instagram-card__content {
    right: 14px;
    bottom: 14px;
    left: 14px;
  }

  .instagram-card__action {
    display: none;
  }

  .instagram-card__number {
    top: 13px;
    left: 13px;

    width: 35px;
    height: 35px;
  }

  .instagram-card__icon {
    width: 38px;
    height: 38px;
  }

  .instagram__profile {
    grid-template-columns: 1fr;
    justify-items: start;

    margin-top: 35px;
    padding: 24px;
  }

  .instagram__profile > p {
    grid-column: auto;
    grid-row: auto;
  }

  .instagram__button {
    width: 100%;
  }

  .instagram__background-word {
    display: none;
  }
}

@media (prefers-reduced-motion: reduce) {
  .instagram-card__image,
  .instagram-card__content,
  .instagram__button,
  .instagram__header-link {
    transition: none;
  }

  .instagram-card:hover .instagram-card__image,
  .instagram-card--brand:hover .instagram-card__image {
    transform: none;
  }
}
</style>