<template>
     <section id="hero" class="section-hero">
        <div class="container">
        <div class="hero-content">
            <p class="hero-eyebrow">
                Next-Generation Engine-Driven Welder
            </p>
            <h1 class="hero-title">
                Power That Goes
                <br>
                <em>Anywhere.</em>
                <br>
                Performs Everywhere.
            </h1>
            <p class="hero-desc">
                Built in Texas. Tested for the toughest environments. 270A at 100% duty cycle and 11kW of generator power — all day, anywhere.
            </p>
            <div class="hero-actions">
                <a href="#demo" class="btn btn-primary btn-sm">Request a Demo</a>
                <a href="#features" class="btn btn-outline btn-sm">See Features ↓</a>
            </div>
        </div>
        <div class="hero-image-wrapper">
            <img src="@/assets/images/ESAB_Ruffian_EMP_270G_EDW_Open_Panel.webp" alt="Hero Image" class="hero-img" loading="lazy"/>
        </div>
        </div>
    </section>
</template>
<style scoped lang="scss">
@use '../../styles/_variables' as *;
.container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: flex-end;
    gap: $sp-6;
    min-height: 440px;
}
@media (max-width: 768px) {
   .container {
        grid-template-columns: 1fr;
    }
}
.hero-content {
    padding-bottom: $sp-8;
}
.hero-tag {
    font-size: $ft-12;
    font-weight: $fw-bold;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: $esab-yellow;
    margin-bottom: $sp-2;
}
.hero-title {
    font-size: 36px;
    font-weight: $fw-bolder;
    line-height: 1.1;
    color: $esab-white;
    margin-bottom: $sp-3;
}
em {
    font-style: normal;
    color: $esab-yellow;
}
.hero-eyebrow {
    font-size: $ft-12;
    font-weight: $fw-bold;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: $esab-yellow;
    margin-bottom: $sp-2;
}
.hero-desc {
    font-size: 18px;
    line-height: 1.4;
    color: $esab-gray-4;
    margin-bottom: $sp-5;
    max-width: 420px;
}
.hero-actions {
    display: flex;
    gap: $sp-2;
    flex-wrap: wrap;
}
a {
    text-decoration: none;
}
.btn-sm {
    padding: 14px 70px;
    font-size: $ft-14;
}
.hero-image-wrapper {
  display: flex;
  align-items: flex-end;
  justify-content: center;
}
.hero-img {
    width: 100%;
    max-width: 500px;
    height: auto;
    object-fit: contain;
    transition: transform 0.4s ease;
}
@media (max-width: 1024px) {
    .hero-img {
        max-width: 400px;
    }
    .hero-actions {
        justify-content: left;
    }
}

@media (max-width: 768px) {
    .hero-actions {
        justify-content: center;
    }
    .hero-image-wrapper {
        justify-content: center;
    }
    .hero-img {
        max-width: 430px;
    }
    .container {
        grid-template-columns: 1fr;
        text-align: center;
    }
    .hero-content {
        padding-bottom: $sp-4;
    }
}
</style>