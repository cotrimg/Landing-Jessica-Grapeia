<script setup>
import SiteHeader from './components/layout/SiteHeader.vue'
import SiteFooter from './components/layout/SiteFooter.vue'

import HeroSection from './components/sections/HeroSection.vue'
import CollectionSection from './components/sections/CollectionSection.vue'
import BrandStorySection from './components/sections/BrandStorySection.vue'
import InstagramSection from './components/sections/InstagramSection.vue'
import ContactSection from './components/sections/ContactSection.vue'
</script>

<template>
  <SiteHeader />

  <main>
    <HeroSection />
    <CollectionSection />
    <BrandStorySection />
    <InstagramSection />
    <ContactSection />
  </main>

  <SiteFooter />
</template>

<style scoped>
.image-test {
  width: min(calc(100% - 40px), 1200px);
  min-height: 80vh;
  margin-inline: auto;
  padding-block: 100px;

  display: grid;
  grid-template-columns: minmax(280px, 500px) 1fr;
  align-items: center;
  gap: clamp(40px, 8vw, 100px);
}

.image-test img {
  width: 100%;
  aspect-ratio: 4 / 5;
  object-fit: cover;
  object-position: center;

  border-radius: 220px 220px 28px 28px;
  box-shadow: 0 30px 70px rgba(112, 38, 78, 0.16);
}

.image-test span {
  color: var(--color-pink-dark);
  font-size: 0.75rem;
  font-weight: 800;
  letter-spacing: 0.18em;
  text-transform: uppercase;
}

.image-test h2 {
  margin-top: 18px;

  font-family: Georgia, 'Times New Roman', serif;
  font-size: clamp(3rem, 6vw, 6rem);
  font-weight: 400;
  line-height: 0.92;
}

.image-test p {
  max-width: 470px;
  margin-top: 24px;

  color: var(--color-muted);
  font-size: 1rem;
  line-height: 1.7;
}

@media (max-width: 760px) {
  .image-test {
    grid-template-columns: 1fr;
    padding-block: 80px;
  }

  .image-test img {
    max-width: 500px;
    justify-self: center;
  }
}
</style>