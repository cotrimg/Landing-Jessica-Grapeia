<script setup>
import {
  onBeforeUnmount,
  onMounted,
  ref,
} from 'vue'

import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sectionElement = ref(null)
const imageElement = ref(null)

let animationContext

onMounted(() => {
  const reduceMotion = window.matchMedia(
    '(prefers-reduced-motion: reduce)'
  ).matches

  if (reduceMotion) {
    return
  }

  animationContext = gsap.context(() => {
    gsap.from('.brand-story__image-frame', {
      opacity: 0,
      x: -80,
      scale: 0.94,
      duration: 1.2,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: sectionElement.value,
        start: 'top 72%',
        once: true,
      },
    })

    gsap.from('.brand-story__eyebrow', {
      opacity: 0,
      y: 25,
      duration: 0.7,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.brand-story__content',
        start: 'top 78%',
        once: true,
      },
    })

    gsap.from('.brand-story__title-line', {
      opacity: 0,
      yPercent: 110,
      rotate: 2,
      duration: 1,
      stagger: 0.12,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.brand-story__title',
        start: 'top 82%',
        once: true,
      },
    })

    gsap.from('.brand-story__text > *', {
      opacity: 0,
      y: 35,
      duration: 0.8,
      stagger: 0.12,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.brand-story__text',
        start: 'top 84%',
        once: true,
      },
    })

    gsap.from('.brand-story__feature', {
      opacity: 0,
      y: 40,
      duration: 0.8,
      stagger: 0.14,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.brand-story__features',
        start: 'top 85%',
        once: true,
      },
    })

    gsap.to(imageElement.value, {
      yPercent: 12,
      ease: 'none',
      scrollTrigger: {
        trigger: sectionElement.value,
        start: 'top bottom',
        end: 'bottom top',
        scrub: 1.2,
      },
    })

    gsap.to('.brand-story__floating-word', {
      xPercent: -18,
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
    id="sobre"
    ref="sectionElement"
    class="brand-story"
    aria-labelledby="brand-story-title"
  >
    <div
      class="brand-story__floating-word"
      aria-hidden="true"
    >
      ESSÊNCIA
    </div>

    <div
      class="brand-story__spark brand-story__spark--one"
      aria-hidden="true"
    >
      ✦
    </div>

    <div
      class="brand-story__spark brand-story__spark--two"
      aria-hidden="true"
    >
      ✧
    </div>

    <div class="brand-story__container">
      <div class="brand-story__visual">
        <div class="brand-story__image-frame">
          <img
            ref="imageElement"
            src="/images/products/colar3.webp"
            alt="Conjunto de joias apresentado em uma embalagem rosa"
            class="brand-story__image"
            width="800"
            height="1000"
            loading="lazy"
          >

          <div class="brand-story__image-overlay"></div>

          <span class="brand-story__image-caption">
            Feito para encantar
          </span>
        </div>

        <div class="brand-story__seal">
          <span>JG</span>

          <small>
            Joias e<br>
            semijoias
          </small>
        </div>

        <div class="brand-story__quote">
          <span aria-hidden="true">“</span>

          <p>
            Um detalhe pode transformar um momento.
          </p>
        </div>
      </div>

      <div class="brand-story__content">
        <span class="brand-story__eyebrow">
          Nossa essência
        </span>

        <h2
          id="brand-story-title"
          class="brand-story__title"
        >
          <span class="brand-story__title-mask">
            <span class="brand-story__title-line">
              Mais que acessórios,
            </span>
          </span>

          <span class="brand-story__title-mask">
            <span
              class="
                brand-story__title-line
                brand-story__title-line--accent
              "
            >
              pequenos significados.
            </span>
          </span>
        </h2>

        <div class="brand-story__text">
          <p>
            A Jessica Grapeia Joias e Semijoias apresenta
            peças escolhidas para acompanhar histórias,
            momentos especiais e diferentes estilos.
          </p>

          <p>
            Cada detalhe, da escolha da peça até a
            apresentação, busca tornar a experiência
            mais delicada, próxima e memorável.
          </p>

          <a
            href="#contato"
            class="brand-story__link"
          >
            Conhecer mais sobre a marca

            <span aria-hidden="true">→</span>
          </a>
        </div>

        <div class="brand-story__features">
          <article class="brand-story__feature">
            <span>01</span>

            <div>
              <h3>Seleção cuidadosa</h3>

              <p>
                Peças escolhidas para combinar delicadeza,
                versatilidade e personalidade.
              </p>
            </div>
          </article>

          <article class="brand-story__feature">
            <span>02</span>

            <div>
              <h3>Apresentação especial</h3>

              <p>
                Uma experiência visual pensada para
                valorizar a peça e o momento de presentear.
              </p>
            </div>
          </article>

          <article class="brand-story__feature">
            <span>03</span>

            <div>
              <h3>Atendimento próximo</h3>

              <p>
                Contato facilitado para ajudar na escolha
                de uma peça especial.
              </p>
            </div>
          </article>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.brand-story {
  position: relative;
  isolation: isolate;
  overflow: hidden;

  padding:
    clamp(110px, 13vw, 190px)
    32px
    clamp(120px, 14vw, 210px);

  color: #fff9fc;

  background:
    radial-gradient(
      circle at 18% 30%,
      rgba(246, 88, 168, 0.14),
      transparent 34%
    ),
    radial-gradient(
      circle at 85% 80%,
      rgba(185, 144, 82, 0.08),
      transparent 28%
    ),
    #241b21;
}

.brand-story__container {
  position: relative;
  z-index: 3;

  width: min(100%, 1320px);
  margin-inline: auto;

  display: grid;
  grid-template-columns:
    minmax(380px, 0.92fr)
    minmax(0, 1.08fr);
  align-items: center;
  gap: clamp(70px, 9vw, 140px);
}

.brand-story__visual {
  position: relative;
  min-height: 760px;

  display: grid;
  place-items: center;
}

.brand-story__image-frame {
  position: relative;
  width: min(88%, 480px);
  height: 650px;
  overflow: hidden;

  border: 7px solid rgba(255, 255, 255, 0.07);
  border-radius: 240px 240px 32px 32px;

  background-color: #392730;

  box-shadow:
    0 45px 100px rgba(0, 0, 0, 0.33),
    0 0 0 1px rgba(255, 255, 255, 0.05);
}

.brand-story__image {
  width: 100%;
  height: 115%;

  object-fit: cover;
  object-position: center;

  transform: translateY(-7%);
  will-change: transform;
}

.brand-story__image-overlay {
  position: absolute;
  inset: 0;

  background:
    linear-gradient(
      to top,
      rgba(24, 13, 20, 0.75),
      transparent 50%
    );

  pointer-events: none;
}

.brand-story__image-caption {
  position: absolute;
  right: 30px;
  bottom: 31px;
  left: 30px;

  color: #ffffff;

  font-size: 0.7rem;
  font-weight: 800;
  letter-spacing: 0.2em;
  text-align: center;
  text-transform: uppercase;
}

.brand-story__seal {
  position: absolute;
  z-index: 4;
  top: 11%;
  right: -2%;

  width: 145px;
  height: 145px;

  display: grid;
  align-content: center;
  justify-items: center;
  gap: 8px;

  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 50%;

  color: #ffffff;

  background:
    linear-gradient(
      145deg,
      rgba(246, 88, 168, 0.88),
      rgba(200, 47, 121, 0.93)
    );

  box-shadow:
    0 26px 60px rgba(0, 0, 0, 0.28);

  transform: rotate(8deg);
}

.brand-story__seal::before {
  content: '';
  position: absolute;
  inset: 8px;

  border: 1px dashed rgba(255, 255, 255, 0.38);
  border-radius: 50%;
}

.brand-story__seal > span {
  position: relative;
  z-index: 2;

  font-family: Georgia, 'Times New Roman', serif;
  font-size: 1.8rem;
}

.brand-story__seal small {
  position: relative;
  z-index: 2;

  font-size: 0.55rem;
  font-weight: 800;
  letter-spacing: 0.13em;
  line-height: 1.45;
  text-align: center;
  text-transform: uppercase;
}

.brand-story__quote {
  position: absolute;
  z-index: 4;
  right: -3%;
  bottom: 8%;

  width: 235px;
  padding: 26px;

  border: 1px solid rgba(255, 255, 255, 0.13);
  border-radius: 25px;

  color: #2f2229;
  background-color: rgba(255, 250, 252, 0.94);

  box-shadow:
    0 28px 60px rgba(0, 0, 0, 0.25);

  backdrop-filter: blur(15px);
}

.brand-story__quote > span {
  display: block;
  height: 34px;

  color: var(--color-pink-dark);

  font-family: Georgia, 'Times New Roman', serif;
  font-size: 3.5rem;
  line-height: 1;
}

.brand-story__quote p {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 1.2rem;
  line-height: 1.35;
}

.brand-story__content {
  position: relative;
  padding-block: 30px;
}

.brand-story__eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 12px;

  margin-bottom: 23px;

  color: #f393c2;

  font-size: 0.72rem;
  font-weight: 800;
  letter-spacing: 0.21em;
  text-transform: uppercase;
}

.brand-story__eyebrow::before {
  content: '';

  width: 38px;
  height: 1px;

  background-color: currentColor;
}

.brand-story__title {
  max-width: 720px;

  font-family: Georgia, 'Times New Roman', serif;
  font-size: clamp(3.2rem, 6vw, 6.3rem);
  font-weight: 400;
  line-height: 0.9;
  letter-spacing: -0.055em;
}

.brand-story__title-mask {
  display: block;
  overflow: hidden;
  padding-bottom: 0.08em;
}

.brand-story__title-line {
  display: block;
  transform-origin: left center;
}

.brand-story__title-line--accent {
  color: #f393c2;
  font-style: italic;
}

.brand-story__text {
  max-width: 620px;
  margin-top: 38px;
}

.brand-story__text p {
  color: rgba(255, 249, 252, 0.68);
  font-size: clamp(0.96rem, 1.3vw, 1.08rem);
  line-height: 1.8;
}

.brand-story__text p + p {
  margin-top: 16px;
}

.brand-story__link {
  display: inline-flex;
  align-items: center;
  gap: 15px;

  margin-top: 29px;
  padding-bottom: 8px;

  border-bottom: 1px solid rgba(243, 147, 194, 0.5);

  color: #f393c2;

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

.brand-story__link:hover {
  gap: 21px;
  color: #ffffff;
  border-color: #ffffff;
}

.brand-story__link:focus-visible {
  outline: 3px solid var(--color-gold);
  outline-offset: 5px;
}

.brand-story__features {
  display: grid;
  gap: 0;

  margin-top: 65px;

  border-top: 1px solid rgba(255, 255, 255, 0.12);
}

.brand-story__feature {
  display: grid;
  grid-template-columns: 58px 1fr;
  gap: 20px;

  padding-block: 25px;

  border-bottom: 1px solid rgba(255, 255, 255, 0.12);
}

.brand-story__feature > span {
  color: #f393c2;

  font-family: Georgia, 'Times New Roman', serif;
  font-size: 1.15rem;
  font-style: italic;
}

.brand-story__feature h3 {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 1.45rem;
  font-weight: 400;
}

.brand-story__feature p {
  max-width: 480px;
  margin-top: 7px;

  color: rgba(255, 249, 252, 0.56);
  font-size: 0.82rem;
  line-height: 1.65;
}

.brand-story__floating-word {
  position: absolute;
  z-index: -1;
  bottom: 0;
  left: 5%;

  color: rgba(255, 255, 255, 0.025);

  font-family: Georgia, 'Times New Roman', serif;
  font-size: clamp(9rem, 22vw, 25rem);
  line-height: 0.7;
  letter-spacing: -0.08em;

  white-space: nowrap;
  pointer-events: none;
  user-select: none;
  will-change: transform;
}

.brand-story__spark {
  position: absolute;
  z-index: 2;

  color: #b99052;
  text-shadow:
    0 0 24px rgba(185, 144, 82, 0.36);

  pointer-events: none;
}

.brand-story__spark--one {
  top: 10%;
  left: 6%;
  font-size: 2rem;
}

.brand-story__spark--two {
  right: 6%;
  bottom: 11%;

  color: #f393c2;
  font-size: 2.7rem;
}

@media (max-width: 1050px) {
  .brand-story__container {
    grid-template-columns: 1fr;
    gap: 75px;
  }

  .brand-story__visual {
    min-height: 680px;
  }

  .brand-story__image-frame {
    width: min(76vw, 470px);
    height: 620px;
  }

  .brand-story__seal {
    right: 14%;
  }

  .brand-story__quote {
    right: 12%;
  }

  .brand-story__content {
    max-width: 780px;
  }
}

@media (max-width: 650px) {
  .brand-story {
    padding:
      90px
      20px
      110px;
  }

  .brand-story__visual {
    min-height: 545px;
  }

  .brand-story__image-frame {
    width: min(88vw, 360px);
    height: 485px;

    border-width: 5px;
    border-radius: 180px 180px 25px 25px;
  }

  .brand-story__seal {
    top: 4%;
    right: -1%;

    width: 105px;
    height: 105px;
  }

  .brand-story__seal > span {
    font-size: 1.35rem;
  }

  .brand-story__seal small {
    font-size: 0.46rem;
  }

  .brand-story__quote {
    right: -1%;
    bottom: 3%;

    width: 185px;
    padding: 19px;
  }

  .brand-story__quote p {
    font-size: 0.98rem;
  }

  .brand-story__title {
    font-size: clamp(3rem, 16vw, 4.8rem);
  }

  .brand-story__features {
    margin-top: 50px;
  }

  .brand-story__feature {
    grid-template-columns: 43px 1fr;
    gap: 13px;
  }

  .brand-story__floating-word {
    display: none;
  }

  .brand-story__spark--one {
    left: 3%;
  }

  .brand-story__spark--two {
    right: 3%;
  }
}
</style>