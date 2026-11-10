<script setup>
import {
  onBeforeUnmount,
  onMounted,
  ref,
} from 'vue'

import { gsap } from 'gsap'

const heroElement = ref(null)
const visualElement = ref(null)
const imageElement = ref(null)
const frontCardElement = ref(null)

let animationContext
let quickImageX
let quickImageY
let quickCardX
let quickCardY

function handlePointerMove(event) {
  const canHover = window.matchMedia(
    '(hover: hover) and (pointer: fine)'
  ).matches

  if (!canHover || !visualElement.value) {
    return
  }

  const bounds =
    visualElement.value.getBoundingClientRect()

  const normalizedX =
    (event.clientX - bounds.left) / bounds.width - 0.5

  const normalizedY =
    (event.clientY - bounds.top) / bounds.height - 0.5

  quickImageX?.(normalizedX * 18)
  quickImageY?.(normalizedY * 18)

  quickCardX?.(normalizedX * -28)
  quickCardY?.(normalizedY * -22)
}

function resetPointerPosition() {
  quickImageX?.(0)
  quickImageY?.(0)

  quickCardX?.(0)
  quickCardY?.(0)
}

onMounted(() => {
  const reduceMotion = window.matchMedia(
    '(prefers-reduced-motion: reduce)'
  ).matches

  animationContext = gsap.context(() => {
    if (reduceMotion) {
      gsap.set(
        [
          '.hero__eyebrow',
          '.hero__title-line',
          '.hero__description',
          '.hero__actions',
          '.hero__benefits',
          '.hero__visual',
        ],
        {
          opacity: 1,
          clearProps: 'transform',
        }
      )

      return
    }

    const timeline = gsap.timeline({
      defaults: {
        ease: 'power3.out',
      },
    })

    timeline
      .from('.hero__eyebrow', {
        opacity: 0,
        y: 25,
        duration: 0.7,
      })
      .from(
        '.hero__title-line',
        {
          opacity: 0,
          yPercent: 110,
          rotate: 2,
          duration: 1.1,
          stagger: 0.12,
        },
        '-=0.35'
      )
      .from(
        '.hero__description',
        {
          opacity: 0,
          y: 35,
          duration: 0.8,
        },
        '-=0.55'
      )
      .from(
        '.hero__actions',
        {
          opacity: 0,
          y: 25,
          duration: 0.7,
        },
        '-=0.5'
      )
      .from(
        '.hero__benefits',
        {
          opacity: 0,
          y: 18,
          duration: 0.6,
        },
        '-=0.4'
      )
      .from(
        '.hero__visual',
        {
          opacity: 0,
          x: 80,
          scale: 0.94,
          duration: 1.3,
        },
        0.2
      )

    gsap.to('.hero__image-frame', {
      y: -12,
      rotate: 1.2,
      duration: 4.2,
      repeat: -1,
      yoyo: true,
      ease: 'sine.inOut',
    })

    gsap.to('.hero__front-card', {
      y: 10,
      rotate: -3,
      duration: 3.6,
      repeat: -1,
      yoyo: true,
      ease: 'sine.inOut',
    })

    gsap.to('.hero__spark', {
      scale: 1.35,
      opacity: 0.45,
      duration: 1.7,
      stagger: 0.25,
      repeat: -1,
      yoyo: true,
      ease: 'sine.inOut',
    })

    quickImageX = gsap.quickTo(
      imageElement.value,
      'x',
      {
        duration: 0.8,
        ease: 'power3.out',
      }
    )

    quickImageY = gsap.quickTo(
      imageElement.value,
      'y',
      {
        duration: 0.8,
        ease: 'power3.out',
      }
    )

    quickCardX = gsap.quickTo(
      frontCardElement.value,
      'x',
      {
        duration: 0.8,
        ease: 'power3.out',
      }
    )

    quickCardY = gsap.quickTo(
      frontCardElement.value,
      'y',
      {
        duration: 0.8,
        ease: 'power3.out',
      }
    )
  }, heroElement.value)
})

onBeforeUnmount(() => {
  animationContext?.revert()
})
</script>

<template>
  <section
    id="inicio"
    ref="heroElement"
    class="hero"
    aria-labelledby="hero-title"
  >
    <div class="hero__background-text">
      BRILHO
    </div>

    <div class="hero__glow hero__glow--one"></div>
    <div class="hero__glow hero__glow--two"></div>

    <div class="hero__container">
      <div class="hero__content">
        <span class="hero__eyebrow">
          Jessica Grapeia Joias
        </span>

        <h1
          id="hero-title"
          class="hero__title"
        >
          <span class="hero__title-mask">
            <span class="hero__title-line">
              Um brilho para
            </span>
          </span>

          <span class="hero__title-mask">
            <span
              class="
                hero__title-line
                hero__title-line--accent
              "
            >
              cada história.
            </span>
          </span>
        </h1>

        <p class="hero__description">
          Joias e semijoias delicadas para celebrar
          momentos, presentear pessoas especiais e
          expressar sua personalidade.
        </p>

        <div class="hero__actions">
          <a
            href="#colecoes"
            class="button button--primary"
          >
            Conhecer as peças

            <span aria-hidden="true">→</span>
          </a>

          <a
            href="#sobre"
            class="button button--secondary"
          >
            Descobrir a marca
          </a>
        </div>

        <ul
          class="hero__benefits"
          aria-label="Diferenciais da marca"
        >
          <li>
            <span aria-hidden="true">✦</span>
            Peças selecionadas
          </li>

          <li>
            <span aria-hidden="true">✦</span>
            Embalagem especial
          </li>

          <li>
            <span aria-hidden="true">✦</span>
            Atendimento personalizado
          </li>
        </ul>
      </div>

      <div
        ref="visualElement"
        class="hero__visual"
        @pointermove="handlePointerMove"
        @pointerleave="resetPointerPosition"
      >
        <div class="hero__decorative-ring"></div>

        <div
          ref="imageElement"
          class="hero__image-frame"
        >
          <img
            src="/images/products/colar1.webp"
            alt="Joia apresentada em uma embalagem rosa em formato de coração"
            class="hero__image"
            width="800"
            height="1000"
            fetchpriority="high"
          >

          <div class="hero__image-shade"></div>

          <span class="hero__image-label">
            Coleção especial
          </span>
        </div>

        <div
          ref="frontCardElement"
          class="hero__front-card"
        >
          <span class="hero__front-card-icon">
            JG
          </span>

          <div>
            <small>Detalhes que</small>
            <strong>encantam</strong>
          </div>
        </div>

        <div class="hero__mini-card">
          <span>01</span>

          <p>
            Escolhas para momentos inesquecíveis
          </p>
        </div>

        <span
          class="hero__spark hero__spark--one"
          aria-hidden="true"
        >
          ✦
        </span>

        <span
          class="hero__spark hero__spark--two"
          aria-hidden="true"
        >
          ✧
        </span>

        <span
          class="hero__spark hero__spark--three"
          aria-hidden="true"
        >
          ✦
        </span>
      </div>
    </div>

    <a
      href="#colecoes"
      class="hero__scroll"
      aria-label="Rolar para conhecer as coleções"
    >
      <span></span>
      Explore
    </a>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  min-height: 100svh;
  overflow: hidden;

  display: flex;
  align-items: center;

  padding: 145px 32px 78px;

  background:
    radial-gradient(
      circle at 72% 34%,
      rgba(246, 88, 168, 0.2),
      transparent 30%
    ),
    radial-gradient(
      circle at 10% 90%,
      rgba(185, 144, 82, 0.08),
      transparent 28%
    ),
    linear-gradient(
      135deg,
      #fffefe 0%,
      #fff7fa 48%,
      #fce3ef 100%
    );
}

.hero__container {
  position: relative;
  z-index: 3;

  width: min(100%, 1320px);
  margin-inline: auto;

  display: grid;
  grid-template-columns:
    minmax(0, 0.95fr)
    minmax(430px, 1.05fr);
  align-items: center;
  gap: clamp(45px, 7vw, 110px);
}

.hero__content {
  position: relative;
  z-index: 5;
  max-width: 680px;
}

.hero__eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 12px;

  margin-bottom: 24px;

  color: var(--color-pink-dark);
  font-size: 0.76rem;
  font-weight: 800;
  letter-spacing: 0.21em;
  text-transform: uppercase;
}

.hero__eyebrow::before {
  content: '';

  width: 38px;
  height: 1px;

  background-color: currentColor;
}

.hero__title {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: clamp(3.8rem, 7.2vw, 7.7rem);
  font-weight: 400;
  line-height: 0.86;
  letter-spacing: -0.06em;
}

.hero__title-mask {
  display: block;
  overflow: hidden;
  padding-bottom: 0.08em;
}

.hero__title-line {
  display: block;
  transform-origin: left center;
}

.hero__title-line--accent {
  color: var(--color-pink-dark);
  font-style: italic;
}

.hero__description {
  max-width: 560px;
  margin-top: 31px;

  color: var(--color-muted);
  font-size: clamp(1rem, 1.4vw, 1.15rem);
  line-height: 1.75;
}

.hero__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 14px;

  margin-top: 37px;
}

.button {
  min-height: 56px;
  padding-inline: 26px;

  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 14px;

  border: 1px solid transparent;
  border-radius: 999px;

  font-size: 0.86rem;
  font-weight: 800;
  text-decoration: none;

  transition:
    transform 200ms ease,
    background-color 200ms ease,
    border-color 200ms ease,
    box-shadow 200ms ease;
}

.button:hover {
  transform: translateY(-3px);
}

.button--primary {
  color: var(--color-white);
  background-color: var(--color-pink-dark);
  box-shadow:
    0 18px 38px rgba(200, 47, 121, 0.22);
}

.button--primary:hover {
  background-color: var(--color-pink);
  box-shadow:
    0 22px 48px rgba(200, 47, 121, 0.3);
}

.button--secondary {
  color: var(--color-text);
  border-color: rgba(40, 34, 40, 0.15);
  background-color: rgba(255, 255, 255, 0.58);
}

.button--secondary:hover {
  border-color: var(--color-pink-dark);
  background-color: var(--color-white);
}

.button:focus-visible {
  outline: 3px solid var(--color-gold);
  outline-offset: 4px;
}

.hero__benefits {
  display: flex;
  flex-wrap: wrap;
  gap: 15px 24px;

  margin-top: 34px;
  padding: 0;

  color: var(--color-muted);
  font-size: 0.74rem;
  font-weight: 700;
  list-style: none;
}

.hero__benefits li {
  display: flex;
  align-items: center;
  gap: 8px;
}

.hero__benefits span {
  color: var(--color-gold);
  font-size: 0.7rem;
}

.hero__visual {
  position: relative;

  min-height: min(70vh, 720px);

  display: grid;
  place-items: center;

  perspective: 1200px;
  isolation: isolate;
}

.hero__image-frame {
  position: relative;
  z-index: 3;

  width: min(66%, 420px);
  aspect-ratio: 4 / 5;
  overflow: hidden;

  border: 8px solid rgba(255, 255, 255, 0.78);
  border-radius: 210px 210px 34px 34px;

  background-color: var(--color-pink-light);

  box-shadow:
    0 45px 90px rgba(104, 36, 73, 0.2),
    0 12px 30px rgba(104, 36, 73, 0.1);

  will-change: transform;
}

.hero__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.hero__image-shade {
  position: absolute;
  inset: 0;

  background:
    linear-gradient(
      to top,
      rgba(38, 16, 29, 0.42),
      transparent 47%
    );

  pointer-events: none;
}

.hero__image-label {
  position: absolute;
  right: 29px;
  bottom: 27px;
  left: 29px;

  color: var(--color-white);
  font-size: 0.68rem;
  font-weight: 800;
  letter-spacing: 0.19em;
  text-align: center;
  text-transform: uppercase;
}

.hero__decorative-ring {
  position: absolute;
  z-index: -1;

  width: min(49vw, 660px);
  aspect-ratio: 1;

  border: 1px solid rgba(200, 47, 121, 0.18);
  border-radius: 50%;

  transform: rotate(-14deg) scaleY(0.82);
}

.hero__decorative-ring::before {
  content: '';
  position: absolute;
  inset: 44px;

  border: 1px solid rgba(185, 144, 82, 0.16);
  border-radius: 50%;
}

.hero__front-card {
  position: absolute;
  z-index: 5;
  right: 3%;
  bottom: 18%;

  width: 210px;
  min-height: 104px;
  padding: 18px;

  display: flex;
  align-items: center;
  gap: 14px;

  border: 1px solid rgba(255, 255, 255, 0.75);
  border-radius: 24px;

  background-color: rgba(255, 255, 255, 0.82);
  box-shadow:
    0 25px 55px rgba(67, 25, 47, 0.17);
  backdrop-filter: blur(18px);

  will-change: transform;
}

.hero__front-card-icon {
  flex: 0 0 auto;

  width: 51px;
  height: 51px;

  display: grid;
  place-items: center;

  border-radius: 50%;

  color: var(--color-white);
  background:
    linear-gradient(
      135deg,
      var(--color-pink),
      var(--color-pink-dark)
    );

  font-family: Georgia, 'Times New Roman', serif;
  font-size: 0.86rem;
}

.hero__front-card div {
  display: grid;
  gap: 2px;
}

.hero__front-card small {
  color: var(--color-muted);
  font-size: 0.67rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}

.hero__front-card strong {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 1.35rem;
  font-weight: 400;
}

.hero__mini-card {
  position: absolute;
  z-index: 4;
  top: 14%;
  left: 0;

  width: 165px;
  padding: 18px;

  border: 1px solid rgba(255, 255, 255, 0.72);
  border-radius: 20px;

  background-color: rgba(255, 255, 255, 0.7);
  box-shadow:
    0 20px 50px rgba(82, 31, 58, 0.1);
  backdrop-filter: blur(15px);
}

.hero__mini-card > span {
  color: var(--color-pink-dark);
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 1.8rem;
}

.hero__mini-card p {
  margin-top: 10px;

  color: var(--color-muted);
  font-size: 0.69rem;
  line-height: 1.5;
}

.hero__spark {
  position: absolute;
  z-index: 6;

  color: var(--color-gold);
  text-shadow:
    0 0 24px rgba(185, 144, 82, 0.52);

  pointer-events: none;
}

.hero__spark--one {
  top: 15%;
  right: 12%;
  font-size: 2rem;
}

.hero__spark--two {
  bottom: 21%;
  left: 10%;
  color: var(--color-pink);
  font-size: 2.8rem;
}

.hero__spark--three {
  right: 18%;
  bottom: 9%;
  font-size: 1.25rem;
}

.hero__background-text {
  position: absolute;
  z-index: 0;
  right: -2%;
  bottom: -3%;

  color: rgba(200, 47, 121, 0.035);

  font-family: Georgia, 'Times New Roman', serif;
  font-size: clamp(8rem, 20vw, 22rem);
  line-height: 0.7;
  letter-spacing: -0.08em;

  pointer-events: none;
  user-select: none;
}

.hero__glow {
  position: absolute;
  border-radius: 50%;
  pointer-events: none;
}

.hero__glow--one {
  top: 12%;
  left: -8%;

  width: 330px;
  height: 330px;

  background-color: rgba(246, 88, 168, 0.07);
  filter: blur(10px);
}

.hero__glow--two {
  right: -8%;
  bottom: -15%;

  width: 450px;
  height: 450px;

  background-color: rgba(185, 144, 82, 0.07);
  filter: blur(10px);
}

.hero__scroll {
  position: absolute;
  z-index: 5;
  bottom: 23px;
  left: 50%;

  display: grid;
  justify-items: center;
  gap: 7px;

  color: var(--color-muted);
  font-size: 0.62rem;
  font-weight: 800;
  letter-spacing: 0.17em;
  text-decoration: none;
  text-transform: uppercase;

  transform: translateX(-50%);
}

.hero__scroll span {
  width: 1px;
  height: 27px;

  background:
    linear-gradient(
      to bottom,
      var(--color-pink-dark),
      transparent
    );
}

@media (max-width: 1050px) {
  .hero {
    padding-top: 135px;
  }

  .hero__container {
    grid-template-columns: 1fr;
    gap: 45px;
  }

  .hero__content {
    max-width: 800px;
  }

  .hero__title {
    font-size: clamp(4rem, 12vw, 7rem);
  }

  .hero__visual {
    min-height: 650px;
  }

  .hero__decorative-ring {
    width: min(84vw, 660px);
  }

  .hero__image-frame {
    width: min(60vw, 410px);
  }

  .hero__mini-card {
    left: 12%;
  }

  .hero__front-card {
    right: 11%;
  }

  .hero__scroll {
    display: none;
  }
}

@media (max-width: 650px) {
  .hero {
    min-height: auto;
    padding: 120px 21px 70px;
  }

  .hero__eyebrow {
    margin-bottom: 18px;
    font-size: 0.67rem;
  }

  .hero__title {
    font-size: clamp(3.2rem, 17vw, 5rem);
    line-height: 0.9;
  }

  .hero__description {
    margin-top: 24px;
    line-height: 1.65;
  }

  .hero__actions {
    display: grid;
  }

  .button {
    width: 100%;
  }

  .hero__benefits {
    display: grid;
  }

  .hero__visual {
    min-height: 490px;
  }

  .hero__image-frame {
    width: min(75vw, 310px);

    border-width: 6px;
    border-radius: 155px 155px 26px 26px;
  }

  .hero__decorative-ring {
    width: min(105vw, 480px);
  }

  .hero__mini-card {
    top: 8%;
    left: -2%;

    width: 135px;
    padding: 14px;
  }

  .hero__mini-card p {
    font-size: 0.62rem;
  }

  .hero__front-card {
    right: -1%;
    bottom: 10%;

    width: 170px;
    min-height: 86px;
    padding: 13px;
  }

  .hero__front-card-icon {
    width: 42px;
    height: 42px;
  }

  .hero__front-card strong {
    font-size: 1.05rem;
  }

  .hero__spark--one {
    right: 2%;
  }

  .hero__spark--two {
    left: 1%;
  }

  .hero__background-text {
    display: none;
  }
}

@media (pointer: coarse) {
  .hero__visual {
    touch-action: pan-y;
  }
}
</style>