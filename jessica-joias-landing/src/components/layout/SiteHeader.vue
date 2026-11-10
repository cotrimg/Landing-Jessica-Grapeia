<script setup>
import {
  onBeforeUnmount,
  onMounted,
  ref,
} from 'vue'

const menuIsOpen = ref(false)
const headerIsScrolled = ref(false)

function toggleMenu() {
  menuIsOpen.value = !menuIsOpen.value
}

function closeMenu() {
  menuIsOpen.value = false
}

function handleScroll() {
  headerIsScrolled.value = window.scrollY > 30
}

function handleEscape(event) {
  if (event.key === 'Escape') {
    closeMenu()
  }
}

onMounted(() => {
  handleScroll()

  window.addEventListener(
    'scroll',
    handleScroll,
    { passive: true },
  )

  window.addEventListener(
    'keydown',
    handleEscape,
  )
})

onBeforeUnmount(() => {
  window.removeEventListener(
    'scroll',
    handleScroll,
  )

  window.removeEventListener(
    'keydown',
    handleEscape,
  )
})
</script>

<template>
  <header
    class="header"
    :class="{
      'header--scrolled': headerIsScrolled,
    }"
  >
    <div class="header__container">
      <a
        href="#inicio"
        class="header__brand"
        aria-label="Jessica Grapeia Joias, ir para o início"
        @click="closeMenu"
      >
        <img
          src="/images/brand/logo-jessica-grapeia.png"
          alt=""
          class="header__monogram"
          width="54"
          height="54"
        >

        <span class="header__brand-name">
          <strong>Jessica Grapeia</strong>
          <small>Joias e Semijoias</small>
        </span>
      </a>

      <nav
        id="main-navigation"
        class="header__navigation"
        :class="{
          'header__navigation--open': menuIsOpen,
        }"
        aria-label="Navegação principal"
      >
        <a
          href="#inicio"
          @click="closeMenu"
        >
          Início
        </a>

        <a
          href="#colecoes"
          @click="closeMenu"
        >
          Coleções
        </a>

        <a
          href="#sobre"
          @click="closeMenu"
        >
          Sobre
        </a>

        <a
          href="#instagram"
          @click="closeMenu"
        >
          Instagram
        </a>

        <a
          href="#contato"
          @click="closeMenu"
        >
          Contato
        </a>
      </nav>

      <div class="header__actions">
        <a
          href="https://jessicagrapeiajoias.lojavirtualnuvem.com.br/"
          target="_blank"
          rel="noopener noreferrer"
          class="header__store-link"
          aria-label="Visitar a loja virtual da Jessica Grapeia"
        >
          Visitar loja

          <span aria-hidden="true">↗</span>
        </a>

        <button
          class="header__menu-button"
          :class="{
            'header__menu-button--open': menuIsOpen,
          }"
          type="button"
          :aria-expanded="menuIsOpen"
          aria-controls="main-navigation"
          :aria-label="
            menuIsOpen
              ? 'Fechar menu'
              : 'Abrir menu'
          "
          @click="toggleMenu"
        >
          <span></span>
          <span></span>
          <span></span>
        </button>
      </div>
    </div>
  </header>
</template>

<style scoped>
.header {
  position: fixed;
  z-index: 1000;
  top: 0;
  left: 0;

  width: 100%;
  padding: 18px 24px;

  pointer-events: none;

  transition:
    padding 250ms ease;
}

.header--scrolled {
  padding-top: 11px;
  padding-bottom: 11px;
}

.header__container {
  position: relative;

  width: min(100%, 1320px);
  min-height: 76px;
  margin-inline: auto;
  padding: 9px 11px 9px 16px;

  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 25px;

  border: 1px solid rgba(255, 255, 255, 0.72);
  border-radius: 999px;

  background-color: rgba(255, 255, 255, 0.72);

  box-shadow:
    0 16px 50px rgba(90, 34, 64, 0.08);

  backdrop-filter: blur(18px);
  -webkit-backdrop-filter: blur(18px);

  pointer-events: auto;

  transition:
    min-height 250ms ease,
    background-color 250ms ease,
    box-shadow 250ms ease,
    border-color 250ms ease;
}

.header--scrolled .header__container {
  min-height: 68px;

  border-color: rgba(200, 47, 121, 0.1);
  background-color: rgba(255, 255, 255, 0.91);

  box-shadow:
    0 14px 45px rgba(78, 28, 55, 0.13);
}

.header__brand {
  min-width: 0;

  display: inline-flex;
  align-items: center;
  gap: 11px;
  flex-shrink: 0;

  color: var(--color-text);
  text-decoration: none;
}

.header__monogram {
  flex: 0 0 auto;

  width: 54px;
  height: 54px;

  display: block;
  object-fit: contain;

  filter:
    drop-shadow(
      0 8px 15px rgba(185, 144, 82, 0.12)
    );

  transition:
    width 250ms ease,
    height 250ms ease,
    transform 250ms ease;
}

.header__brand:hover .header__monogram {
  transform: translateY(-2px) rotate(-2deg);
}

.header--scrolled .header__monogram {
  width: 48px;
  height: 48px;
}

.header__brand-name {
  min-width: 0;

  display: grid;
  gap: 3px;
}

.header__brand-name strong {
  overflow: hidden;

  color: var(--color-pink-dark);

  font-family:
    Georgia,
    'Times New Roman',
    serif;
  font-size: 1.04rem;
  font-weight: 500;
  line-height: 1;
  letter-spacing: 0.015em;

  text-overflow: ellipsis;
  white-space: nowrap;
}

.header__brand-name small {
  color: var(--color-gold);

  font-size: 0.58rem;
  font-weight: 800;
  letter-spacing: 0.15em;
  line-height: 1.2;
  text-transform: uppercase;
  white-space: nowrap;
}

.header__navigation {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: clamp(15px, 1.7vw, 29px);
}

.header__navigation a {
  position: relative;

  padding-block: 10px;

  color: var(--color-text);
  font-size: 0.79rem;
  font-weight: 700;
  text-decoration: none;
  white-space: nowrap;
}

.header__navigation a::after {
  content: '';

  position: absolute;
  right: 0;
  bottom: 4px;
  left: 0;

  height: 2px;
  border-radius: 999px;

  background:
    linear-gradient(
      90deg,
      var(--color-pink-dark),
      var(--color-gold)
    );

  transform: scaleX(0);
  transform-origin: right;

  transition:
    transform 220ms ease;
}

.header__navigation a:hover::after,
.header__navigation a:focus-visible::after {
  transform: scaleX(1);
  transform-origin: left;
}

.header__actions {
  display: flex;
  align-items: center;
  gap: 11px;
  flex-shrink: 0;
}

.header__store-link {
  min-height: 48px;
  padding: 0 19px;

  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 10px;

  border-radius: 999px;

  color: var(--color-white);

  background:
    linear-gradient(
      135deg,
      var(--color-pink-dark),
      var(--color-pink)
    );

  box-shadow:
    0 12px 26px rgba(200, 47, 121, 0.2);

  font-size: 0.76rem;
  font-weight: 800;
  text-decoration: none;
  white-space: nowrap;

  transition:
    transform 180ms ease,
    box-shadow 180ms ease,
    filter 180ms ease;
}

.header__store-link:hover {
  transform: translateY(-2px);

  filter: saturate(1.08);

  box-shadow:
    0 16px 32px rgba(200, 47, 121, 0.28);
}

.header__menu-button {
  position: relative;

  width: 46px;
  height: 46px;

  display: none;
  place-items: center;

  padding: 12px;
  border: 0;
  border-radius: 50%;

  color: var(--color-text);
  background-color: var(--color-pink-light);

  cursor: pointer;
}

.header__menu-button span {
  position: absolute;

  width: 20px;
  height: 2px;

  border-radius: 999px;
  background-color: currentColor;

  transition:
    transform 220ms ease,
    opacity 180ms ease,
    top 220ms ease;
}

.header__menu-button span:nth-child(1) {
  top: 15px;
}

.header__menu-button span:nth-child(2) {
  top: 22px;
}

.header__menu-button span:nth-child(3) {
  top: 29px;
}

.header__menu-button--open span:nth-child(1) {
  top: 22px;
  transform: rotate(45deg);
}

.header__menu-button--open span:nth-child(2) {
  opacity: 0;
  transform: scaleX(0);
}

.header__menu-button--open span:nth-child(3) {
  top: 22px;
  transform: rotate(-45deg);
}

.header a:focus-visible,
.header button:focus-visible {
  outline: 3px solid var(--color-gold);
  outline-offset: 3px;
}

@media (max-width: 1080px) {
  .header__navigation {
    position: absolute;
    top: calc(100% + 12px);
    right: 0;
    left: 0;

    display: grid;
    gap: 4px;

    padding: 17px;

    border:
      1px solid rgba(200, 47, 121, 0.12);
    border-radius: 26px;

    background-color: rgba(255, 255, 255, 0.97);

    box-shadow:
      0 24px 60px rgba(90, 34, 64, 0.15);

    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);

    opacity: 0;
    visibility: hidden;

    transform: translateY(-10px);

    transition:
      opacity 180ms ease,
      visibility 180ms ease,
      transform 180ms ease;
  }

  .header__navigation--open {
    opacity: 1;
    visibility: visible;
    transform: translateY(0);
  }

  .header__navigation a {
    padding: 13px 16px;
    border-radius: 14px;
  }

  .header__navigation a:hover {
    color: var(--color-pink-dark);
    background-color: var(--color-pink-light);
  }

  .header__navigation a::after {
    display: none;
  }

  .header__menu-button {
    display: grid;
  }
}

@media (max-width: 650px) {
  .header {
    padding: 11px;
  }

  .header--scrolled {
    padding: 8px 11px;
  }

  .header__container,
  .header--scrolled .header__container {
    min-height: 64px;
    padding: 7px 8px 7px 11px;
  }

  .header__brand {
    gap: 8px;
  }

  .header__monogram,
  .header--scrolled .header__monogram {
    width: 43px;
    height: 43px;
  }

  .header__brand-name strong {
    max-width: 145px;
    font-size: 0.86rem;
  }

  .header__brand-name small {
    display: none;
  }

  .header__store-link {
    display: none;
  }

  .header__menu-button {
    width: 44px;
    height: 44px;
  }

  .header__menu-button span:nth-child(1) {
    top: 14px;
  }

  .header__menu-button span:nth-child(2) {
    top: 21px;
  }

  .header__menu-button span:nth-child(3) {
    top: 28px;
  }

  .header__menu-button--open span:nth-child(1),
  .header__menu-button--open span:nth-child(3) {
    top: 21px;
  }
}

@media (max-width: 390px) {
  .header__brand-name strong {
    max-width: 110px;
    font-size: 0.78rem;
  }
}

@media (prefers-reduced-motion: reduce) {
  .header,
  .header__container,
  .header__monogram,
  .header__navigation,
  .header__navigation a::after,
  .header__store-link,
  .header__menu-button span {
    transition: none;
  }
}
</style>