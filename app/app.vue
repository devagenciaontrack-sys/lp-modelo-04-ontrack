<script setup lang="ts">
// ============ PERSONALIZAÇÃO ============
const site = {
  marca: 'Sua Marca',
  subtitulo: 'Estética avançada',
  whatsapp: '5500000000000',
  instagram: '#',
  endereco: 'Rua Exemplo, 000 — Bairro, Cidade/UF',
  responsavel: 'Dra. Nome Sobrenome · CRM/CRO 00000',
  // vídeo de fundo do topo (mp4 curto, sem som). Deixe vazio para usar o fundo animado.
  videoTopo: '',
}
const wa = (msg = 'Olá! Gostaria de agendar uma avaliação.') => `https://wa.me/${site.whatsapp}?text=${encodeURIComponent(msg)}`

const procedimentos = [
  { t: 'Harmonização facial', d: 'Equilíbrio dos traços com resultado natural.', s: 'g-a' },
  { t: 'Bioestimuladores', d: 'Firmeza e qualidade da pele a médio prazo.', s: 'g-b' },
  { t: 'Skinbooster', d: 'Hidratação profunda e viço.', s: 'g-c' },
  { t: 'Toxina botulínica', d: 'Suavização de linhas de expressão.', s: 'g-d' },
  { t: 'Peeling', d: 'Renovação e uniformização do tom.', s: 'g-e' },
]
const depoimentos = [
  { n: 'Camila R.', p: 'Harmonização facial' },
  { n: 'Fernanda L.', p: 'Bioestimulador' },
  { n: 'Patrícia M.', p: 'Skinbooster' },
]

const pos = ref(50)
</script>

<template>
  <div>
    <header class="top">
      <div class="wrap top-in">
        <nav class="nav nav-l"><a href="#resultados">Resultados</a><a href="#procedimentos">Procedimentos</a></nav>
        <a href="#" class="logo"><b>{{ site.marca }}</b><small>{{ site.subtitulo }}</small></a>
        <nav class="nav nav-r"><a href="#espaco">O espaço</a><a :href="wa()" target="_blank" rel="noopener" class="nav-cta">Agendar</a></nav>
      </div>
    </header>

    <main>
      <section class="hero">
        <video v-if="site.videoTopo" class="hero-media" :src="site.videoTopo" autoplay muted loop playsinline />
        <div v-else class="hero-media hero-fallback" aria-hidden="true"><span /><span /><span /></div>
        <div class="hero-in">
          <p class="eyebrow">{{ site.subtitulo }}</p>
          <h1>Beleza que parece <i>sua</i>, só que descansada.</h1>
          <p class="lead">Procedimentos pensados a partir das proporções do seu rosto, para um resultado que ninguém aponta, só elogia.</p>
          <a class="btn btn-dark" :href="wa()" target="_blank" rel="noopener">Agendar avaliação</a>
        </div>
      </section>

      <section id="resultados" class="sec">
        <div class="wrap ba-grid">
          <div>
            <p class="eyebrow eyebrow-dark">Antes e depois</p>
            <h2>Arraste e veja a diferença.</h2>
            <p class="muted">Resultados reais variam de pessoa para pessoa. Imagens publicadas com autorização das pacientes.</p>
          </div>
          <div class="ba" :style="{ '--pos': pos + '%' }">
            <div class="ba-img ba-before"><span>Antes</span></div>
            <div class="ba-img ba-after"><span>Depois</span></div>
            <div class="ba-handle" aria-hidden="true"><i /></div>
            <input v-model.number="pos" type="range" min="0" max="100" aria-label="Comparar antes e depois">
          </div>
        </div>
      </section>

      <section id="procedimentos" class="sec proc">
        <div class="wrap">
          <h2 class="center">Procedimentos</h2>
          <div class="mag">
            <a v-for="(p, i) in procedimentos" :key="p.t" :href="wa(`Olá! Quero saber mais sobre ${p.t}.`)" target="_blank" rel="noopener" class="mag-item" :class="`m-${i}`">
              <div class="mag-img" :class="p.s" />
              <div class="mag-txt"><span class="mag-n">{{ String(i + 1).padStart(2, '0') }}</span><h3>{{ p.t }}</h3><p>{{ p.d }}</p></div>
            </a>
          </div>
        </div>
      </section>

      <section id="espaco" class="sec space">
        <div class="wrap space-grid">
          <div class="space-txt">
            <h2>O espaço</h2>
            <p>Um ambiente reservado, com sala de recepção privativa, café e tempo para conversar antes de qualquer procedimento.</p>
            <ul><li>Atendimento com hora marcada</li><li>Sala de procedimentos individual</li><li>Retorno incluso em cada protocolo</li></ul>
          </div>
          <div class="ph ph-1"><span>Recepção</span></div>
          <div class="ph ph-2"><span>Sala de procedimentos</span></div>
          <div class="ph ph-3"><span>Detalhe do ambiente</span></div>
        </div>
      </section>

      <section class="sec">
        <div class="wrap">
          <h2 class="center">Quem viveu a experiência</h2>
          <div class="videos">
            <button v-for="d in depoimentos" :key="d.n" class="vcard" type="button">
              <span class="vplay" />
              <span class="vmeta"><b>{{ d.n }}</b>{{ d.p }}</span>
            </button>
          </div>
          <p class="note center">Espaço para vídeos curtos de pacientes (até 30 segundos, formato vertical).</p>
        </div>
      </section>

      <section class="concierge">
        <div class="wrap concierge-in">
          <h2>Sua avaliação começa por uma conversa.</h2>
          <p>A nossa concierge responde pelo WhatsApp e encontra o melhor horário para você.</p>
          <a class="btn btn-light" :href="wa()" target="_blank" rel="noopener">Falar com a concierge</a>
        </div>
      </section>
    </main>

    <footer class="foot">
      <div class="wrap foot-in"><b>{{ site.marca }}</b><span>{{ site.endereco }}</span><span>Responsável técnica: {{ site.responsavel }}</span><a :href="site.instagram">Instagram</a></div>
    </footer>
  </div>
</template>
