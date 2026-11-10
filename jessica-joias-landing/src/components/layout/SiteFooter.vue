<script setup>
const currentYear = new Date().getFullYear()

const storeUrl =
  'https://jessicagrapeiajoias.lojavirtualnuvem.com.br/'

const instagramUrl =
  'https://www.instagram.com/jessicagrapeiajoias/'

const whatsappUrl =
  'https://wa.me/5511941323134?text=Ol%C3%A1%21%20Conheci%20a%20Jessica%20Grapeia%20Joias%20pelo%20site%20e%20gostaria%20de%20conhecer%20as%20pe%C3%A7as.'
</script>

<template>
  <footer class="footer">
    <div
      class="footer__background-word"
      aria-hidden="true"
    >
      JESSICA
    </div>

    <div class="footer__spark footer__spark--one">
      ✦
    </div>

    <div class="footer__spark footer__spark--two">
      ✧
    </div>

    <div class="footer__container">
      <div class="footer__top">
        <div class="footer__brand-column">
          <a
            href="#inicio"
            class="footer__brand"
            aria-label="Jessica Grapeia Joias, voltar ao início"
          >
            <img
              src="/images/brand/logo-jessica-grapeia.png"
              alt=""
              class="footer__monogram"
              width="88"
              height="88"
            >

            <span class="footer__brand-name">
              <strong>Jessica Grapeia</strong>
              <small>Joias e Semijoias</small>
            </span>
          </a>

          <p class="footer__slogan">
            Elegância que revela sua essência.
          </p>

          <p class="footer__description">
            Peças delicadas para celebrar momentos,
            expressar sua personalidade e transformar
            detalhes em lembranças especiais.
          </p>

          <div
            class="footer__social-links"
            aria-label="Redes e canais da marca"
          >
            <a
              :href="instagramUrl"
              target="_blank"
              rel="noopener noreferrer"
              class="footer__social-link"
              aria-label="Acessar o Instagram da Jessica Grapeia Joias"
            >
              <svg
                viewBox="0 0 24 24"
                aria-hidden="true"
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
                  class="footer__icon-dot"
                />
              </svg>
            </a>

            <a
              :href="whatsappUrl"
              target="_blank"
              rel="noopener noreferrer"
              class="footer__social-link"
              aria-label="Conversar com a Jessica Grapeia Joias pelo WhatsApp"
            >
              <svg
                viewBox="0 0 24 24"
                aria-hidden="true"
              >
                <path
                  d="
                    M20.5 11.8
                    A8.5 8.5 0 0 1 8 19.3
                    L3.5 20.5
                    L4.8 16.2
                    A8.5 8.5 0 1 1 20.5 11.8
                    Z
                  "
                />

                <path
                  d="
                    M8.2 7.7
                    C8.5 11.2 11.2 13.9 14.7 14.3
                    L16.1 12.9
                    C16.5 12.5 17 12.6 17.4 12.8
                    L19 13.6
                    C19.4 13.8 19.5 14.2 19.4 14.6
                    C19 16.1 17.6 17 16.1 17
                    C10.8 16.6 6 11.9 5.6 6.6
                    C5.6 5.1 6.5 3.7 8 3.3
                    C8.4 3.2 8.8 3.3 9 3.7
                    L9.8 5.3
                    C10 5.7 10.1 6.2 9.7 6.6
                    Z
                  "
                />
              </svg>
            </a>

            <a
              :href="storeUrl"
              target="_blank"
              rel="noopener noreferrer"
              class="footer__social-link"
              aria-label="Acessar a loja virtual da Jessica Grapeia"
            >
              <svg
                viewBox="0 0 24 24"
                aria-hidden="true"
              >
                <path d="M5 9.5V21h14V9.5" />
                <path d="M3.5 9.5 5 4h14l1.5 5.5" />
                <path d="M3.5 9.5c0 1.4 1.1 2.5 2.5 2.5s2.5-1.1 2.5-2.5" />
                <path d="M8.5 9.5c0 1.4 1.1 2.5 2.5 2.5s2.5-1.1 2.5-2.5" />
                <path d="M13.5 9.5c0 1.4 1.1 2.5 2.5 2.5s2.5-1.1 2.5-2.5" />
                <path d="M8.5 21v-5h7v5" />
              </svg>
            </a>
          </div>
        </div>

        <div class="footer__navigation">
          <div class="footer__column">
            <h2>Navegação</h2>

            <nav aria-label="Navegação do rodapé">
              <a href="#inicio">Início</a>
              <a href="#colecoes">Coleções</a>
              <a href="#sobre">Sobre a marca</a>
              <a href="#instagram">Instagram</a>
              <a href="#contato">Contato</a>
            </nav>
          </div>

          <div class="footer__column">
            <h2>Descubra</h2>

            <nav aria-label="Links comerciais">
              <a
                :href="storeUrl"
                target="_blank"
                rel="noopener noreferrer"
              >
                Loja virtual
                <span aria-hidden="true">↗</span>
              </a>

              <a
                :href="instagramUrl"
                target="_blank"
                rel="noopener noreferrer"
              >
                Novidades
                <span aria-hidden="true">↗</span>
              </a>

              <a
                :href="whatsappUrl"
                target="_blank"
                rel="noopener noreferrer"
              >
                Atendimento
                <span aria-hidden="true">↗</span>
              </a>
            </nav>
          </div>

          <div class="footer__column footer__column--contact">
            <h2>Vamos conversar?</h2>

            <p>
              Precisa de ajuda para escolher uma peça
              ou presente especial?
            </p>

            <a
              :href="whatsappUrl"
              target="_blank"
              rel="noopener noreferrer"
              class="footer__contact-button"
            >
              Falar pelo WhatsApp

              <span aria-hidden="true">→</span>
            </a>

            <div class="footer__profile">
              <span>Instagram</span>

              <a
                :href="instagramUrl"
                target="_blank"
                rel="noopener noreferrer"
              >
                @jessicagrapeiajoias
              </a>
            </div>
          </div>
        </div>
      </div>

      <div class="footer__divider">
        <span></span>
        <span aria-hidden="true">✦</span>
        <span></span>
      </div>

      <div class="footer__bottom">
        <p>
          © {{ currentYear }} Jessica Grapeia Joias.
          Todos os direitos reservados.
        </p>

        <div class="footer__legal">
          <a href="#">
            Política de privacidade
          </a>

          <a href="#">
            Termos de uso
          </a>
        </div>

        <a
          href="#inicio"
          class="footer__back-to-top"
          aria-label="Voltar ao início da página"
        >
          Voltar ao topo

          <span aria-hidden="true">↑</span>
        </a>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  position: relative;
  isolation: isolate;
  overflow: hidden;

  padding:
    clamp(90px, 11vw, 150px)
    32px
    32px;

  color: #fff9fc;

  background:
    radial-gradient(
      circle at 12% 18%,
      rgba(246, 88, 168, 0.14),
      transparent 28%
    ),
    radial-gradient(
      circle at 86% 80%,
      rgba(185, 144, 82, 0.1),
      transparent 26%
    ),
    #1d161a;
}

.footer__container {
  position: relative;
  z-index: 2;

  width: min(100%, 1320px);
  margin-inline: auto;
}

.footer__top {
  display: grid;
  grid-template-columns:
    minmax(280px, 0.8fr)
    minmax(0, 1.2fr);
  gap: clamp(70px, 10vw, 150px);
}

.footer__brand-column {
  max-width: 420px;
}

.footer__brand {
  display: inline-flex;
  align-items: center;
  gap: 16px;

  color: inherit;
  text-decoration: none;
}

.footer__monogram {
  flex: 0 0 auto;

  width: 88px;
  height: 88px;

  object-fit: contain;

  filter:
    drop-shadow(
      0 15px 25px rgba(185, 144, 82, 0.18)
    );

  transition:
    transform 250ms ease;
}

.footer__brand:hover .footer__monogram {
  transform:
    translateY(-3px)
    rotate(-2deg);
}

.footer__brand-name {
  display: grid;
  gap: 6px;
}

.footer__brand-name strong {
  color: #f393c2;

  font-family:
    Georgia,
    'Times New Roman',
    serif;
  font-size: clamp(1.45rem, 2vw, 2rem);
  font-weight: 400;
  line-height: 1;
}

.footer__brand-name small {
  color: #c6a06a;

  font-size: 0.61rem;
  font-weight: 800;
  letter-spacing: 0.18em;
  text-transform: uppercase;
}

.footer__slogan {
  margin-top: 35px;

  color: #f3b0d1;

  font-family:
    Georgia,
    'Times New Roman',
    serif;
  font-size: clamp(1.6rem, 2.7vw, 2.6rem);
  font-style: italic;
  line-height: 1.12;
}

.footer__description {
  max-width: 390px;
  margin-top: 20px;

  color: rgba(255, 249, 252, 0.58);
  font-size: 0.87rem;
  line-height: 1.75;
}

.footer__social-links {
  display: flex;
  flex-wrap: wrap;
  gap: 11px;

  margin-top: 30px;
}

.footer__social-link {
  width: 47px;
  height: 47px;

  display: grid;
  place-items: center;

  border:
    1px solid rgba(255, 255, 255, 0.14);
  border-radius: 50%;

  color: #f3b0d1;
  background-color: rgba(255, 255, 255, 0.045);

  transition:
    color 200ms ease,
    border-color 200ms ease,
    background-color 200ms ease,
    transform 200ms ease;
}

.footer__social-link:hover {
  color: #20161b;
  border-color: #f3b0d1;
  background-color: #f3b0d1;

  transform: translateY(-3px);
}

.footer__social-link svg {
  width: 20px;
  height: 20px;

  fill: none;
  stroke: currentColor;
  stroke-width: 1.6;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.footer__icon-dot {
  fill: currentColor;
  stroke: none;
}

.footer__navigation {
  display: grid;
  grid-template-columns:
    minmax(120px, 0.7fr)
    minmax(120px, 0.8fr)
    minmax(230px, 1.2fr);
  gap: clamp(35px, 6vw, 80px);
}

.footer__column h2 {
  margin-bottom: 25px;

  color: #ffffff;

  font-size: 0.68rem;
  font-weight: 800;
  letter-spacing: 0.18em;
  text-transform: uppercase;
}

.footer__column nav {
  display: grid;
  justify-items: start;
  gap: 15px;
}

.footer__column nav a {
  position: relative;

  display: inline-flex;
  align-items: center;
  gap: 9px;

  color: rgba(255, 249, 252, 0.6);

  font-size: 0.82rem;
  line-height: 1.4;
  text-decoration: none;

  transition:
    color 200ms ease,
    transform 200ms ease;
}

.footer__column nav a:hover {
  color: #f3b0d1;
  transform: translateX(4px);
}

.footer__column--contact > p {
  max-width: 290px;

  color: rgba(255, 249, 252, 0.56);
  font-size: 0.84rem;
  line-height: 1.7;
}

.footer__contact-button {
  min-height: 52px;
  margin-top: 24px;
  padding: 0 21px;

  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 14px;

  border-radius: 999px;

  color: #1f151a;

  background:
    linear-gradient(
      135deg,
      #f3b0d1,
      #c6a06a
    );

  box-shadow:
    0 16px 36px rgba(0, 0, 0, 0.2);

  font-size: 0.77rem;
  font-weight: 800;
  text-decoration: none;

  transition:
    transform 200ms ease,
    box-shadow 200ms ease,
    filter 200ms ease;
}

.footer__contact-button:hover {
  transform: translateY(-3px);
  filter: brightness(1.08);

  box-shadow:
    0 21px 45px rgba(0, 0, 0, 0.28);
}

.footer__profile {
  display: grid;
  gap: 6px;

  margin-top: 26px;
}

.footer__profile span {
  color: rgba(255, 249, 252, 0.38);

  font-size: 0.59rem;
  font-weight: 800;
  letter-spacing: 0.16em;
  text-transform: uppercase;
}

.footer__profile a {
  color: #f3b0d1;
  font-size: 0.8rem;
  text-decoration: none;
}

.footer__profile a:hover {
  text-decoration: underline;
  text-underline-offset: 4px;
}

.footer__divider {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  gap: 18px;

  margin-block:
    clamp(65px, 8vw, 105px)
    27px;
}

.footer__divider span:first-child,
.footer__divider span:last-child {
  height: 1px;
  background-color:
    rgba(255, 255, 255, 0.1);
}

.footer__divider span:nth-child(2) {
  color: #c6a06a;
  font-size: 0.86rem;
}

.footer__bottom {
  display: grid;
  grid-template-columns:
    minmax(220px, 1fr)
    auto
    minmax(150px, 1fr);
  align-items: center;
  gap: 30px;
}

.footer__bottom > p {
  color: rgba(255, 249, 252, 0.38);
  font-size: 0.69rem;
  line-height: 1.6;
}

.footer__legal {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 19px;
}

.footer__legal a,
.footer__back-to-top {
  color: rgba(255, 249, 252, 0.48);
  font-size: 0.68rem;
  text-decoration: none;

  transition:
    color 200ms ease;
}

.footer__legal a:hover,
.footer__back-to-top:hover {
  color: #f3b0d1;
}

.footer__back-to-top {
  display: inline-flex;
  align-items: center;
  justify-self: end;
  gap: 10px;

  font-weight: 700;
}

.footer__back-to-top span {
  width: 31px;
  height: 31px;

  display: grid;
  place-items: center;

  border:
    1px solid rgba(255, 255, 255, 0.13);
  border-radius: 50%;

  color: #f3b0d1;

  transition:
    color 200ms ease,
    border-color 200ms ease,
    background-color 200ms ease,
    transform 200ms ease;
}

.footer__back-to-top:hover span {
  color: #1f151a;
  border-color: #f3b0d1;
  background-color: #f3b0d1;

  transform: translateY(-3px);
}

.footer__background-word {
  position: absolute;
  z-index: -1;
  right: -3%;
  bottom: 5%;

  color: rgba(255, 255, 255, 0.018);

  font-family:
    Georgia,
    'Times New Roman',
    serif;
  font-size: clamp(10rem, 24vw, 28rem);
  line-height: 0.7;
  letter-spacing: -0.08em;

  pointer-events: none;
  user-select: none;
}

.footer__spark {
  position: absolute;
  z-index: 1;

  color: #c6a06a;
  text-shadow:
    0 0 22px rgba(198, 160, 106, 0.32);

  pointer-events: none;
}

.footer__spark--one {
  top: 12%;
  right: 7%;
  font-size: 1.8rem;
}

.footer__spark--two {
  bottom: 19%;
  left: 4%;

  color: #f393c2;
  font-size: 2.4rem;
}

.footer a:focus-visible {
  outline: 3px solid #c6a06a;
  outline-offset: 4px;
}

@media (max-width: 1050px) {
  .footer__top {
    grid-template-columns: 1fr;
    gap: 70px;
  }

  .footer__brand-column {
    max-width: 570px;
  }

  .footer__navigation {
    grid-template-columns:
      repeat(3, 1fr);
  }
}

@media (max-width: 720px) {
  .footer {
    padding:
      80px
      20px
      27px;
  }

  .footer__brand {
    align-items: flex-start;
  }

  .footer__monogram {
    width: 72px;
    height: 72px;
  }

  .footer__navigation {
    grid-template-columns:
      repeat(2, 1fr);
    gap: 50px 35px;
  }

  .footer__column--contact {
    grid-column: 1 / -1;
  }

  .footer__bottom {
    grid-template-columns: 1fr;
    justify-items: start;
    gap: 19px;
  }

  .footer__legal {
    justify-content: flex-start;
  }

  .footer__back-to-top {
    justify-self: start;
  }

  .footer__background-word {
    display: none;
  }
}

@media (max-width: 460px) {
  .footer__brand {
    display: grid;
  }

  .footer__brand-name strong {
    font-size: 1.45rem;
  }

  .footer__navigation {
    grid-template-columns: 1fr;
    gap: 43px;
  }

  .footer__column--contact {
    grid-column: auto;
  }

  .footer__contact-button {
    width: 100%;
  }

  .footer__legal {
    display: grid;
    gap: 12px;
  }
}

@media (prefers-reduced-motion: reduce) {
  .footer__monogram,
  .footer__social-link,
  .footer__column nav a,
  .footer__contact-button,
  .footer__back-to-top span {
    transition: none;
  }
}
</style>