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
  cnpj: '00.000.000/0000-00',
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
const entrevista = [
  { q: 'O resultado fica artificial?', a: 'Não é o que buscamos. Trabalhamos com doses e técnicas que respeitam os seus traços. A ideia é que as pessoas notem que você está bem, sem saber exatamente o porquê.' },
  { q: 'Dói?', a: 'Usamos anestésico tópico e técnicas de conforto. A maioria das pacientes descreve como uma leve pressão.' },
  { q: 'Em quanto tempo vejo o resultado?', a: 'Depende do procedimento: alguns aparecem na hora, outros se completam em duas a quatro semanas. Explicamos tudo na avaliação.' },
  { q: 'Posso voltar ao trabalho no mesmo dia?', a: 'Na maioria dos procedimentos, sim. Quando há algum cuidado especial, você recebe as orientações por escrito.' },
  { q: 'De quanto em quanto tempo preciso repetir?', a: 'Varia de procedimento para procedimento: alguns duram de quatro a seis meses, outros mais de um ano. Você sai da avaliação com um calendário pensado para você.' },
  { q: 'A avaliação é obrigatória?', a: 'Sim. É nela que entendemos o que você deseja, avaliamos a pele e indicamos o que faz sentido, inclusive quando a resposta é não fazer nada.' },
]
</script>

<template>
  <div>
    <header class="top">
      <div class="wrap top-in">
        <nav class="nav nav-l"><a href="#resultados">Resultados</a><a href="#procedimentos">Procedimentos</a></nav>
        <a href="#" class="logo"><b>{{ site.marca }}</b><small>{{ site.subtitulo }}</small></a>
        <nav class="nav nav-r"><a href="#sobre">Sobre nós</a><a :href="wa()" target="_blank" rel="noopener" class="nav-cta">Agendar</a></nav>
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

      <!-- sobre nós -->
      <!-- TODO: trocar pela história real da clínica e pela foto da responsável técnica -->
      <section id="sobre" class="sec about">
        <div class="wrap about-grid">
          <div class="ph about-ph"><span>Foto da responsável técnica</span></div>
          <div class="about-txt">
            <h2>Sobre nós</h2>
            <p>A {{ site.marca }} nasceu da vontade de fazer estética com calma: avaliação antes de qualquer agulha, protocolo explicado em detalhe e resultado que respeita os traços de cada pessoa.</p>
            <blockquote>“Prefiro dizer não a um procedimento a fazer algo que não combina com o seu rosto.”</blockquote>
            <p class="about-sign">{{ site.responsavel }}</p>
            <dl class="about-facts">
              <div><dt>Desde</dt><dd>2016</dd></div>
              <div><dt>Atendimento</dt><dd>Só com hora marcada</dd></div>
              <div><dt>Avaliação</dt><dd>Individual</dd></div>
            </dl>
          </div>
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

      <section id="perguntas" class="sec entrevista">
        <div class="wrap">
          <h2 class="center">Perguntas que você talvez tenha vergonha de fazer</h2>
          <p class="ent-sub">Respondidas pela nossa responsável técnica, {{ site.responsavel.split(' · ')[0] }}.</p>
          <div class="ent-colunas">
            <article v-for="e in entrevista" :key="e.q" class="ent">
              <p class="ent-q"><span aria-hidden="true">P.</span>{{ e.q }}</p>
              <p class="ent-a"><span aria-hidden="true">R.</span>{{ e.a }}</p>
            </article>
          </div>
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

    <footer class="foot rod">
      <div class="wrap rod-top">
        <div class="rod-brand">
          <b class="rod-logo">{{ site.marca }}</b>
          <p>{{ site.endereco }}</p><p>Responsável técnica: {{ site.responsavel }} · CNPJ {{ site.cnpj }}</p>
        </div>
        <div class="rod-soc">
          <a :href="`https://wa.me/${site.whatsapp}`" target="_blank" rel="noopener" aria-label="WhatsApp"><svg viewBox="0 0 24 24" aria-hidden="true"><path fill="currentColor" stroke="none" d="M12 2.2a9.7 9.7 0 0 0-8.3 14.7L2.3 21.8l5-1.3A9.7 9.7 0 1 0 12 2.2Zm0 17.7a8 8 0 0 1-4.1-1.1l-.3-.2-3 .8.8-2.9-.2-.3A8 8 0 1 1 12 19.9Zm4.4-6c-.2-.1-1.4-.7-1.7-.8-.2-.1-.4-.1-.5.1l-.8 1c-.1.2-.3.2-.5.1a6.6 6.6 0 0 1-3.3-2.9c-.2-.4.2-.4.7-1.3.1-.2 0-.3 0-.4l-.8-1.8c-.2-.5-.4-.4-.5-.4h-.5a.9.9 0 0 0-.7.3 2.8 2.8 0 0 0-.9 2.1 4.9 4.9 0 0 0 1 2.6 11.2 11.2 0 0 0 4.3 3.8c1.6.7 2.2.7 3 .6.5-.1 1.4-.6 1.6-1.2.2-.6.2-1.1.1-1.2l-.5-.4Z"/></svg></a>
          <a :href="site.instagram" target="_blank" rel="noopener" aria-label="Instagram"><svg viewBox="0 0 24 24" aria-hidden="true"><rect x="3.5" y="3.5" width="17" height="17" rx="5"/><circle cx="12" cy="12" r="4"/><circle cx="17.2" cy="6.8" r=".6"/></svg></a>
        </div>
      </div>
      <div class="wrap"><div class="rod-bot">
        <span>© {{ new Date().getFullYear() }} {{ site.marca }}. Todos os direitos reservados.</span>
        <a class="rod-credit" href="https://www.ontrackagenciadigital.com.br/" target="_blank" rel="noopener">Desenvolvido por <b>OnTrack Agência Digital</b></a>
      </div></div>
    </footer>
  </div>
</template>
