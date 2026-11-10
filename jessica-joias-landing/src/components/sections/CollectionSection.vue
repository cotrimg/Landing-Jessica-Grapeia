<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

import { products } from '../../data/products'

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
    gsap.from('.collections__eyebrow', {
      opacity: 0,
      y: 25,
      duration: 0.7,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.collections__header',
        start: 'top 85%',
        once: true,
      },
    })

    gsap.from('.collections__title', {
      opacity: 0,
      y: 55,
      duration: 1,
      delay: 0.1,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.collections__header',
        start: 'top 85%',
        once: true,
      },
    })

    gsap.from('.collections__description', {
      opacity: 0,
      y: 35,
      duration: 0.8,
      delay: 0.25,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.collections__header',
        start: 'top 85%',
        once: true,
      },
    })

    gsap.from('.product-card', {
      opacity: 0,
      y: 80,
      scale: 0.96,
      duration: 0.9,
      stagger: 0.12,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.collections__grid',
        start: 'top 78%',
        once: true,
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
    id="colecoes"
    ref="sectionElement"
    class="collections"
    aria-labelledby="collections-title"
  >
    <div class="collections__container">
      <header class="collections__header">
        <div class="collections__heading">
          <span class="collections__eyebrow">
            Escolha seu brilho
          </span>

          <h2
            id="collections-title"
            class="collections__title"
          >
            Delicadeza em
            <em>cada detalhe.</em>
          </h2>
        </div>

        <div class="collections__description">
          <p>
            Conheça uma seleção de peças que combina elegância,
            personalidade e cuidado em cada apresentação.
          </p>

          <a href="#" class="collections__all-link">
            Ver catálogo completo
            <span aria-hidden="true">↗</span>
          </a>
        </div>
      </header>

      <div class="collections__grid">
        <article
          v-for="(product, index) in products"
          :key="product.id"
          class="product-card"
        >
          <a
            :href="product.link"
            class="product-card__link"
            :aria-label="`Conhecer ${product.name}`"
          >
            <div class="product-card__visual">
              <img
                :src="product.image"
                :alt="product.name"
                :style="{
                  objectPosition: product.imagePosition,
                }"
                class="product-card__image"
                loading="lazy"
                width="800"
                height="1000"
              >

              <div class="product-card__overlay"></div>

              <span class="product-card__number">
                {{ String(index + 1).padStart(2, '0') }}
              </span>

              <span class="product-card__explore">
                Explorar
                <span aria-hidden="true">↗</span>
              </span>
            </div>

            <div class="product-card__content">
              <span class="product-card__category">
                {{ product.category }}
              </span>

              <h3>{{ product.name }}</h3>

              <p>{{ product.description }}</p>
            </div>
          </a>
        </article>
      </div>

      <footer class="collections__footer">
        <div class="collections__footer-line"></div>

        <p>
          Peças escolhidas para acompanhar histórias especiais.
        </p>

        <a href="#" class="collections__button">
          Visitar a loja
          <span aria-hidden="true">→</span>
        </a>
      </footer>
    </div>
  </section>
</template>

<style scoped>
.collections {
  position: relative;
  overflow: hidden;
  padding: clamp(100px, 12vw, 180px) 32px;
  background:
    linear-gradient(
      180deg,
      #fffafb 0%,
      #ffffff 35%,
      #fff9fc 100%
    );
}

.collections::before {
  content: '';
  position: absolute;
  top: 2%;
  right: -190px;

  width: 430px;
  height: 430px;

  border: 1px solid rgba(200, 47, 121, 0.1);
  border-radius: 50%;
  pointer-events: none;
}

.collections::after {
  content: '';
  position: absolute;
  bottom: 10%;
  left: -230px;

  width: 420px;
  height: 420px;

  border-radius: 50%;

  background-color: rgba(246, 88, 168, 0.04);
  filter: blur(2px);
  pointer-events: none;
}

.collections__container {
  position: relative;
  z-index: 2;

  width: min(100%, 1320px);
  margin-inline: auto;
}

.collections__header {
  display: grid;
  grid-template-columns: minmax(0, 1.25fr) minmax(280px, 0.75fr);
  align-items: end;
  gap: clamp(40px, 8vw, 110px);

  margin-bottom: clamp(65px, 9vw, 115px);
}

.collections__eyebrow {
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

.collections__eyebrow::before {
  content: '';
  display: block;

  width: 38px;
  height: 1px;

  background-color: currentColor;
}

.collections__title {
  max-width: 780px;

  font-family: Georgia, 'Times New Roman', serif;
  font-size: clamp(3.4rem, 7vw, 7rem);
  font-weight: 400;
  line-height: 0.86;
  letter-spacing: -0.055em;
}

.collections__title em {
  display: block;
  color: var(--color-pink-dark);
  font-weight: 400;
}

.collections__description {
  padding-bottom: 8px;
}

.collections__description p {
  color: var(--color-muted);
  font-size: 1rem;
  line-height: 1.75;
}

.collections__all-link {
  display: inline-flex;
  align-items: center;
  gap: 13px;

  margin-top: 25px;
  padding-bottom: 7px;

  border-bottom: 1px solid rgba(40, 34, 40, 0.25);

  color: var(--color-text);
  font-size: 0.78rem;
  font-weight: 800;
  letter-spacing: 0.08em;
  text-decoration: none;
  text-transform: uppercase;

  transition:
    color 200ms ease,
    border-color 200ms ease;
}

.collections__all-link:hover {
  color: var(--color-pink-dark);
  border-color: var(--color-pink-dark);
}

.collections__grid {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 70px 28px;
  align-items: start;
}

.product-card {
  grid-column: span 4;
}

.product-card:nth-child(2),
.product-card:nth-child(5) {
  transform: translateY(70px);
}

.product-card__link {
  display: block;
  color: inherit;
  text-decoration: none;
}

.product-card__visual {
  position: relative;
  overflow: hidden;
  aspect-ratio: 4 / 5;

  border-radius: 190px 190px 26px 26px;

  background:
    linear-gradient(
      145deg,
      var(--color-pink-light),
      #f8c5dc
    );

  box-shadow: 0 28px 60px rgba(102, 40, 72, 0.11);

  isolation: isolate;
}

.product-card__image {
  width: 100%;
  height: 100%;
  object-fit: cover;

  transition:
    transform 900ms cubic-bezier(0.16, 1, 0.3, 1),
    filter 500ms ease;
}

.product-card__overlay {
  position: absolute;
  z-index: 1;
  inset: 0;

  background:
    linear-gradient(
      to top,
      rgba(31, 15, 24, 0.56) 0%,
      rgba(31, 15, 24, 0.04) 50%,
      transparent 75%
    );

  opacity: 0.75;

  transition: opacity 400ms ease;
}

.product-card__number {
  position: absolute;
  z-index: 2;
  top: 25px;
  left: 25px;

  width: 48px;
  height: 48px;

  display: grid;
  place-items: center;

  border: 1px solid rgba(255, 255, 255, 0.65);
  border-radius: 50%;

  color: var(--color-white);
  background-color: rgba(255, 255, 255, 0.16);
  backdrop-filter: blur(10px);

  font-size: 0.7rem;
  font-weight: 800;
  letter-spacing: 0.1em;
}

.product-card__explore {
  position: absolute;
  z-index: 2;
  right: 24px;
  bottom: 24px;
  left: 24px;

  display: flex;
  align-items: center;
  justify-content: space-between;

  color: var(--color-white);
  font-size: 0.7rem;
  font-weight: 800;
  letter-spacing: 0.15em;
  text-transform: uppercase;
}

.product-card__explore > span {
  width: 45px;
  height: 45px;

  display: grid;
  place-items: center;

  border-radius: 50%;

  color: var(--color-pink-dark);
  background-color: var(--color-white);

  font-size: 1rem;

  transition:
    color 300ms ease,
    background-color 300ms ease,
    transform 400ms ease;
}

.product-card__content {
  padding: 26px 7px 0;
}

.product-card__category {
  color: var(--color-pink-dark);

  font-size: 0.67rem;
  font-weight: 800;
  letter-spacing: 0.17em;
  text-transform: uppercase;
}

.product-card__content h3 {
  margin-top: 9px;

  font-family: Georgia, 'Times New Roman', serif;
  font-size: clamp(1.9rem, 3vw, 2.65rem);
  font-weight: 400;
  line-height: 1;
}

.product-card__content p {
  max-width: 355px;
  margin-top: 13px;

  color: var(--color-muted);
  font-size: 0.88rem;
  line-height: 1.65;
}

.product-card__link:hover .product-card__image {
  transform: scale(1.075);
}

.product-card__link:hover .product-card__overlay {
  opacity: 1;
}

.product-card__link:hover
.product-card__explore > span {
  color: var(--color-white);
  background-color: var(--color-pink-dark);
  transform: rotate(45deg);
}

.product-card__link:focus-visible {
  border-radius: 190px 190px 26px 26px;
  outline: 3px solid var(--color-gold);
  outline-offset: 7px;
}

.collections__footer {
  display: grid;
  grid-template-columns: minmax(70px, 1fr) auto auto;
  align-items: center;
  gap: 25px;

  margin-top: clamp(120px, 13vw, 180px);
}

.collections__footer-line {
  height: 1px;
  background-color: rgba(40, 34, 40, 0.14);
}

.collections__footer p {
  color: var(--color-muted);
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 1rem;
  font-style: italic;
}

.collections__button {
  min-height: 54px;
  padding: 0 23px;

  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 16px;

  border: 1px solid rgba(40, 34, 40, 0.15);
  border-radius: 999px;

  color: var(--color-text);
  background-color: var(--color-white);

  font-size: 0.8rem;
  font-weight: 800;
  text-decoration: none;

  transition:
    color 200ms ease,
    border-color 200ms ease,
    background-color 200ms ease,
    transform 200ms ease;
}

.collections__button:hover {
  color: var(--color-white);
  border-color: var(--color-pink-dark);
  background-color: var(--color-pink-dark);
  transform: translateY(-3px);
}

.collections__button:focus-visible,
.collections__all-link:focus-visible {
  outline: 3px solid var(--color-gold);
  outline-offset: 4px;
}

@media (max-width: 950px) {
  .collections__header {
    grid-template-columns: 1fr;
    gap: 30px;
  }

  .collections__description {
    max-width: 580px;
  }

  .collections__grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .product-card {
    grid-column: auto;
  }

  .product-card:nth-child(2),
  .product-card:nth-child(5) {
    transform: translateY(50px);
  }

  .collections__footer {
    grid-template-columns: 1fr auto;
  }

  .collections__footer-line {
    display: none;
  }
}

@media (max-width: 600px) {
  .collections {
    padding-inline: 20px;
  }

  .collections__header {
    margin-bottom: 55px;
  }

  .collections__title {
    font-size: clamp(3.2rem, 17vw, 5.2rem);
  }

  .collections__grid {
    grid-template-columns: 1fr;
    gap: 58px;
  }

  .product-card:nth-child(2),
  .product-card:nth-child(5) {
    transform: none;
  }

  .product-card__visual {
    border-radius: 150px 150px 23px 23px;
  }

  .collections__footer {
    grid-template-columns: 1fr;
    justify-items: start;
    margin-top: 80px;
  }

  .collections__button {
    width: 100%;
  }
}
</style>