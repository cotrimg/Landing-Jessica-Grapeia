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

let animationContext

onMounted(() => {
  const reduceMotion = window.matchMedia(
    '(prefers-reduced-motion: reduce)'
  ).matches

  if (reduceMotion) {
    return
  }

  animationContext = gsap.context(() => {
    gsap.from('.contact__eyebrow', {
      opacity: 0,
      y: 25,
      duration: 0.7,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.contact__content',
        start: 'top 82%',
        once: true,
      },
    })

    gsap.from('.contact__title-line', {
      opacity: 0,
      yPercent: 110,
      rotate: 2,
      duration: 1,
      stagger: 0.12,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.contact__title',
        start: 'top 84%',
        once: true,
      },
    })

    gsap.from('.contact__description', {
      opacity: 0,
      y: 35,
      duration: 0.8,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.contact__description',
        start: 'top 87%',
        once: true,
      },
    })

    gsap.from('.contact__actions', {
      opacity: 0,
      y: 30,
      duration: 0.8,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.contact__actions',
        start: 'top 88%',
        once: true,
      },
    })

    gsap.from('.contact__benefit', {
      opacity: 0,
      y: 35,
      duration: 0.75,
      stagger: 0.13,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.contact__benefits',
        start: 'top 88%',
        once: true,
      },
    })

    gsap.from('.contact__visual', {
      opacity: 0,
      x: 70,
      scale: 0.95,
      duration: 1.2,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.contact__visual',
        start: 'top 78%',
        once: true,
      },
    })

    gsap.to('.contact__visual-image', {
      yPercent: 10,
      ease: 'none',
      scrollTrigger: {
        trigger: sectionElement.value,
        start: 'top bottom',
        end: 'bottom top',
        scrub: 1.2,
      },
    })

    gsap.to('.contact__marquee-content', {
      xPercent: -50,
      duration: 24,
      repeat: -1,
      ease: 'none',
    })
  }, sectionElement.value)
})

onBeforeUnmount(() => {
  animationContext?.revert()
})
</script>

<template>
  <section
    id="contato"
    ref="sectionElement"
    class="contact"
    aria-labelledby="contact-title"
  >
    <div class="contact__marquee">
      <div class="contact__marquee-content">
        <span>Joias para momentos especiais</span>
        <span aria-hidden="true">✦</span>

        <span>Delicadeza em cada detalhe</span>
        <span aria-hidden="true">✦</span>

        <span>Escolha seu brilho</span>
        <span aria-hidden="true">✦</span>

        <span>Joias para momentos especiais</span>
        <span aria-hidden="true">✦</span>

        <span>Delicadeza em cada detalhe</span>
        <span aria-hidden="true">✦</span>

        <span>Escolha seu brilho</span>
        <span aria-hidden="true">✦</span>
      </div>
    </div>

    <div class="contact__container">
      <div class="contact__content">
        <span class="contact__eyebrow">
          Encontre sua peça
        </span>

        <h2
          id="contact-title"
          class="contact__title"
        >
          <span class="contact__title-mask">
            <span class="contact__title-line">
              Um detalhe especial
            </span>
          </span>

          <span class="contact__title-mask">
            <span
              class="
                contact__title-line
                contact__title-line--accent
              "
            >
              espera por você.
            </span>
          </span>
        </h2>

        <p class="contact__description">
          Conheça as peças disponíveis na loja ou converse
          pelo WhatsApp para receber ajuda na escolha de um
          presente ou de uma joia especial.
        </p>

        <div class="contact__actions">
          <a
            href="https://jessicagrapeiajoias.lojavirtualnuvem.com.br/"
            target="_blank"
            rel="noopener noreferrer"
            class="contact__button contact__button--primary"
          >
            Visitar a loja

            <span aria-hidden="true">↗</span>
          </a>

          <a
            href="#"
            class="
              contact__button
              contact__button--whatsapp
            "
            aria-label="Conversar pelo WhatsApp"
          >
            <span
              class="contact__whatsapp-icon"
              aria-hidden="true"
            >
              ☏
            </span>

            Falar pelo WhatsApp
          </a>
        </div>

        <div class="contact__benefits">
          <article class="contact__benefit">
            <span aria-hidden="true">01</span>

            <div>
              <h3>Escolha facilitada</h3>

              <p>
                Receba ajuda para encontrar uma peça que
                combine com o estilo ou a ocasião.
              </p>
            </div>
          </article>

          <article class="contact__benefit">
            <span aria-hidden="true">02</span>

            <div>
              <h3>Compra pela loja</h3>

              <p>
                Consulte produtos, informações e condições
                diretamente no catálogo virtual.
              </p>
            </div>
          </article>

          <article class="contact__benefit">
            <span aria-hidden="true">03</span>

            <div>
              <h3>Atendimento próximo</h3>

              <p>
                Converse diretamente pelo WhatsApp para
                esclarecer dúvidas antes da compra.
              </p>
            </div>
          </article>
        </div>
      </div>

      <div class="contact__visual">
        <div class="contact__visual-frame">
          <img
            src="/images/products/colar4.webp"
            alt="Colar delicado apresentado sobre uma almofada rosa"
            class="contact__visual-image"
            width="800"
            height="1000"
            loading="lazy"
          >

          <div class="contact__visual-overlay"></div>
        </div>

        <div class="contact__visual-card">
          <span>✦</span>

          <p>
            Descubra peças que combinam com você.
          </p>
        </div>

        <div
          class="contact__decorative-circle"
          aria-hidden="true"
        ></div>

        <span
          class="contact__spark contact__spark--one"
          aria-hidden="true"
        >
          ✦
        </span>

        <span
          class="contact__spark contact__spark--two"
          aria-hidden="true"
        >
          ✧
        </span>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact {
  position: relative;
  overflow: hidden;

  padding:
    0
    32px
    clamp(110px, 13vw, 190px);

  background:
    radial-gradient(
      circle at 84% 40%,
      rgba(246, 88, 168, 0.17),
      transparent 28%
    ),
    linear-gradient(
      145deg,
      #fffefe 0%,
      #fff7fa 55%,
      #fce7f1 100%
    );
}

.contact__marquee {
  width: calc(100% + 64px);
  margin-left: -32px;
  margin-bottom: clamp(90px, 11vw, 150px);

  overflow: hidden;

  border-top: 1px solid rgba(200, 47, 121, 0.13);
  border-bottom: 1px solid rgba(200, 47, 121, 0.13);

  background-color: rgba(255, 255, 255, 0.5);
}

.contact__marquee-content {
  width: max-content;
  min-width: 200%;

  display: flex;
  align-items: center;
  justify-content: space-around;
  gap: 46px;

  padding-block: 24px;

  color: var(--color-pink-dark);

  font-family: Georgia, 'Times New Roman', serif;
  font-size: clamp(1.25rem, 2.3vw, 2.1rem);
  font-style: italic;
  white-space: nowrap;

  will-change: transform;
}

.contact__marquee-content > span:nth-child(even) {
  color: var(--color-gold);
  font-size: 0.85rem;
}

.contact__container {
  position: relative;
  z-index: 2;

  width: min(100%, 1320px);
  margin-inline: auto;

  display: grid;
  grid-template-columns:
    minmax(0, 1.05fr)
    minmax(390px, 0.95fr);
  align-items: center;
  gap: clamp(65px, 9vw, 135px);
}

.contact__content {
  max-width: 730px;
}

.contact__eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 12px;

  margin-bottom: 23px;

  color: var(--color-pink-dark);
  font-size: 0.73rem;
  font-weight: 800;
  letter-spacing: 0.21em;
  text-transform: uppercase;
}

.contact__eyebrow::before {
  content: '';

  width: 38px;
  height: 1px;

  background-color: currentColor;
}

.contact__title {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: clamp(3.3rem, 6.4vw, 6.8rem);
  font-weight: 400;
  line-height: 0.88;
  letter-spacing: -0.055em;
}

.contact__title-mask {
  display: block;
  overflow: hidden;
  padding-bottom: 0.08em;
}

.contact__title-line {
  display: block;
  transform-origin: left center;
}

.contact__title-line--accent {
  color: var(--color-pink-dark);
  font-style: italic;
}

.contact__description {
  max-width: 600px;
  margin-top: 32px;

  color: var(--color-muted);
  font-size: clamp(0.98rem, 1.3vw, 1.1rem);
  line-height: 1.78;
}

.contact__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 14px;

  margin-top: 37px;
}

.contact__button {
  min-height: 56px;
  padding: 0 25px;

  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 13px;

  border: 1px solid transparent;
  border-radius: 999px;

  font-size: 0.84rem;
  font-weight: 800;
  text-decoration: none;

  transition:
    color 200ms ease,
    background-color 200ms ease,
    border-color 200ms ease,
    box-shadow 200ms ease,
    transform 200ms ease;
}

.contact__button:hover {
  transform: translateY(-3px);
}

.contact__button--primary {
  color: var(--color-white);
  background-color: var(--color-pink-dark);

  box-shadow:
    0 18px 40px rgba(200, 47, 121, 0.22);
}

.contact__button--primary:hover {
  background-color: var(--color-pink);

  box-shadow:
    0 23px 48px rgba(200, 47, 121, 0.3);
}

.contact__button--whatsapp {
  color: #156b42;

  border-color: rgba(21, 107, 66, 0.22);
  background-color: rgba(255, 255, 255, 0.72);
}

.contact__button--whatsapp:hover {
  color: #ffffff;
  border-color: #168a50;
  background-color: #168a50;
}

.contact__button:focus-visible {
  outline: 3px solid var(--color-gold);
  outline-offset: 4px;
}

.contact__whatsapp-icon {
  font-size: 1.05rem;
}

.contact__benefits {
  display: grid;
  gap: 0;

  margin-top: 65px;

  border-top: 1px solid rgba(40, 34, 40, 0.12);
}

.contact__benefit {
  display: grid;
  grid-template-columns: 50px 1fr;
  gap: 20px;

  padding-block: 23px;

  border-bottom: 1px solid rgba(40, 34, 40, 0.12);
}

.contact__benefit > span {
  color: var(--color-pink-dark);

  font-family: Georgia, 'Times New Roman', serif;
  font-size: 1.05rem;
  font-style: italic;
}

.contact__benefit h3 {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 1.38rem;
  font-weight: 400;
}

.contact__benefit p {
  max-width: 500px;
  margin-top: 6px;

  color: var(--color-muted);
  font-size: 0.81rem;
  line-height: 1.6;
}

.contact__visual {
  position: relative;

  min-height: 680px;

  display: grid;
  place-items: center;

  isolation: isolate;
}

.contact__visual-frame {
  position: relative;
  z-index: 3;

  width: min(82%, 450px);
  height: 610px;

  overflow: hidden;

  border: 7px solid rgba(255, 255, 255, 0.8);
  border-radius: 225px 225px 31px 31px;

  background-color: var(--color-pink-light);

  box-shadow:
    0 42px 90px rgba(104, 36, 73, 0.2);
}

.contact__visual-image {
  width: 100%;
  height: 115%;

  object-fit: cover;
  object-position: center;

  transform: translateY(-7%);
  will-change: transform;
}

.contact__visual-overlay {
  position: absolute;
  inset: 0;

  background:
    linear-gradient(
      to top,
      rgba(50, 22, 37, 0.4),
      transparent 44%
    );

  pointer-events: none;
}

.contact__visual-card {
  position: absolute;
  z-index: 5;
  right: -4%;
  bottom: 11%;

  width: 220px;
  padding: 24px;

  border: 1px solid rgba(255, 255, 255, 0.78);
  border-radius: 25px;

  background-color: rgba(255, 255, 255, 0.9);

  box-shadow:
    0 28px 60px rgba(82, 31, 58, 0.17);

  backdrop-filter: blur(16px);
}

.contact__visual-card span {
  color: var(--color-gold);
  font-size: 1.4rem;
}

.contact__visual-card p {
  margin-top: 10px;

  color: var(--color-text);

  font-family: Georgia, 'Times New Roman', serif;
  font-size: 1.2rem;
  line-height: 1.35;
}

.contact__decorative-circle {
  position: absolute;
  z-index: 1;

  width: min(43vw, 590px);
  aspect-ratio: 1;

  border: 1px solid rgba(200, 47, 121, 0.15);
  border-radius: 50%;

  transform: rotate(12deg) scaleY(0.84);
}

.contact__decorative-circle::before {
  content: '';
  position: absolute;
  inset: 43px;

  border: 1px dashed rgba(185, 144, 82, 0.18);
  border-radius: 50%;
}

.contact__spark {
  position: absolute;
  z-index: 5;

  color: var(--color-gold);

  text-shadow:
    0 0 22px rgba(185, 144, 82, 0.4);

  pointer-events: none;
}

.contact__spark--one {
  top: 10%;
  right: 7%;

  font-size: 2rem;
}

.contact__spark--two {
  bottom: 19%;
  left: 3%;

  color: var(--color-pink);
  font-size: 2.7rem;
}

@media (max-width: 1050px) {
  .contact__container {
    grid-template-columns: 1fr;
    gap: 75px;
  }

  .contact__content {
    max-width: 790px;
  }

  .contact__visual {
    min-height: 650px;
  }

  .contact__visual-frame {
    width: min(70vw, 450px);
  }

  .contact__decorative-circle {
    width: min(83vw, 590px);
  }

  .contact__visual-card {
    right: 13%;
  }
}

@media (max-width: 650px) {
  .contact {
    padding:
      0
      20px
      105px;
  }

  .contact__marquee {
    width: calc(100% + 40px);
    margin-left: -20px;
    margin-bottom: 85px;
  }

  .contact__marquee-content {
    gap: 30px;
    padding-block: 20px;
  }

  .contact__title {
    font-size: clamp(3.1rem, 16vw, 4.9rem);
  }

  .contact__actions {
    display: grid;
  }

  .contact__button {
    width: 100%;
  }

  .contact__benefits {
    margin-top: 50px;
  }

  .contact__benefit {
    grid-template-columns: 42px 1fr;
    gap: 13px;
  }

  .contact__visual {
    min-height: 520px;
  }

  .contact__visual-frame {
    width: min(88vw, 355px);
    height: 485px;

    border-width: 5px;
    border-radius: 178px 178px 25px 25px;
  }

  .contact__decorative-circle {
    width: min(110vw, 480px);
  }

  .contact__visual-card {
    right: -2%;
    bottom: 3%;

    width: 180px;
    padding: 18px;
  }

  .contact__visual-card p {
    font-size: 1rem;
  }

  .contact__spark--one {
    right: 1%;
  }

  .contact__spark--two {
    left: 0;
  }
}
</style>