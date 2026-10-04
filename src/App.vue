<script setup>
import { computed, nextTick, ref, onMounted, onBeforeUnmount } from "vue";
import Lenis from "lenis";
let lenis;
onMounted(() => {
  lenis = new Lenis({
    autoRaf: true,
    anchors: { offset: -18 },
    lerp: 0.085,
    respectReducedMotion: true,
    prevent: (node) => Boolean(node.closest?.("dialog")),
  });
});
onBeforeUnmount(() => lenis?.destroy());
const intention = ref("Rotina mais leve");
const intentions = [
  {
    title: "Rotina mais leve",
    text: "Um corte que faça sentido com o tempo que você tem para cuidar dos fios. Conte como costuma lavar, secar e finalizar seu cabelo.",
    service: 0,
  },
  {
    title: "Uma nova cor",
    text: "Traga uma referência do resultado que deseja e conte o histórico de coloração. A condição dos fios e a manutenção orientam a proposta.",
    service: 1,
  },
  {
    title: "Uma ocasião especial",
    text: "Pense no horário, na roupa e no movimento que você quer para os fios. Uma referência ajuda a conversar sobre a finalização.",
    service: 4,
  },
];
const intentionDetail = computed(() =>
  intentions.find((item) => item.title === intention.value),
);
function prepareIntention() {
  chooseService(intentionDetail.value.service);
  lenis?.scrollTo("#servicos", { offset: -18 });
}
const journalIndex = ref(0);
const journal = [
  {
    title: "No seu dia a dia",
    heading: "O acabamento começa na rotina.",
    text: "Um cabelo bonito também precisa funcionar fora do salão. Observe como seus fios se comportam e leve essa conversa para a próxima visita.",
    tips: [
      "Conte quanto tempo você costuma dedicar à finalização e quais ferramentas já usa.",
      "Peça ao profissional para demonstrar uma maneira de reproduzir o acabamento em casa.",
    ],
  },
  {
    title: "Entre colorações",
    heading: "Uma cor pensada para durar.",
    text: "A manutenção faz parte da escolha da cor. Antes de mudar, converse sobre o crescimento da raiz, os reflexos desejados e a frequência de retorno.",
    tips: [
      "Guarde uma foto da cor em luz natural para acompanhar como os reflexos mudam.",
      "Defina com seu profissional a rotina de manutenção adequada ao procedimento realizado.",
    ],
  },
  {
    title: "Sua textura natural",
    heading: "Movimento que respeita os fios.",
    text: "Liso, ondulado ou cacheado: o ponto de partida é entender a textura, o volume e o resultado que você gosta de ver no espelho.",
    tips: [
      "Traga uma referência com textura parecida com a sua, além do formato que deseja.",
      "Mostre o cabelo como costuma usar no cotidiano para orientar o corte e a finalização.",
    ],
  },
];
const menuOpen = ref(false);
const menuButton = ref(null);
const openingNav = ref(null);
function toggleMenu() {
  menuOpen.value = !menuOpen.value;
  if (menuOpen.value)
    nextTick(() => openingNav.value?.querySelector("a")?.focus());
}
function dismissMenu() {
  menuOpen.value = false;
  nextTick(() => menuButton.value?.focus());
}
const selectedService = ref(0);
const booking = ref(null);
const confirmed = ref(false);
const name = ref("");
const date = ref("");
const period = ref("Manhã");
const bookingService = ref("Corte & forma");
const now = new Date();
const today = `${now.getFullYear()}-${String(now.getMonth() + 1).padStart(2, "0")}-${String(now.getDate()).padStart(2, "0")}`;
const services = [
  {
    name: "Corte & forma",
    hint: "Proporção e movimento",
    description:
      "Um corte pensado para a textura do seu cabelo, seu estilo e a maneira como você gosta de finalizar os fios.",
    detail: "Conversa de estilo, lavagem, corte e finalização.",
    duration: "Cerca de 1 hora",
  },
  {
    name: "Cor & luz",
    hint: "Nuances que valorizam",
    description:
      "Uma proposta de cor construída a partir dos seus traços, da condição dos fios e da manutenção que cabe na sua rotina.",
    detail: "Avaliação, planejamento da cor e finalização.",
    duration: "Tempo após avaliação",
  },
  {
    name: "Luzes & reflexos",
    hint: "Profundidade e delicadeza",
    description:
      "Reflexos e iluminação em pontos escolhidos para trazer dimensão ao cabelo. A técnica é definida em uma avaliação dos fios.",
    detail:
      "Avaliação dos fios, escolha da técnica e orientação de manutenção.",
    duration: "Tempo após avaliação",
  },
  {
    name: "Cuidado & textura",
    hint: "Respeito à sua natureza",
    description:
      "Um ritual de cuidado e finalização que considera a textura natural e as necessidades dos seus fios.",
    detail: "Avaliação, lavagem, cuidado e orientação de finalização.",
    duration: "Cerca de 1 hora",
  },
  {
    name: "Finalização",
    hint: "Seu cabelo, outra ocasião",
    description:
      "Ondas, escova ou uma finalização que preserve o movimento natural. Traga a ocasião e a referência que você tem em mente.",
    detail: "Conversa sobre o estilo desejado e finalização personalizada.",
    duration: "Tempo conforme o estilo",
  },
  {
    name: "Consulta de estilo",
    hint: "O começo da conversa",
    description:
      "Um encontro para olhar suas referências, entender sua rotina e preparar uma proposta de corte, cor e cuidado.",
    detail: "Conversa, avaliação visual e proposta individual.",
    duration: "Cerca de 30 minutos",
  },
];
const activeService = computed(() => services[selectedService.value]);
let previousFocus;
function openBooking(service) {
  bookingService.value = service || activeService.value.name;
  confirmed.value = false;
  menuOpen.value = false;
  previousFocus = document.activeElement;
  lenis?.stop();
  booking.value.showModal();
  document.body.classList.add("modal-open");
  nextTick(() => booking.value.querySelector("input")?.focus());
}
function closeDialog(dialog) {
  dialog.close();
}
function afterClose() {
  document.body.classList.remove("modal-open");
  lenis?.start();
  previousFocus?.focus();
}
function submitPreference() {
  const input = booking.value.querySelector("#guest-name");
  if (!name.value.trim()) {
    input.setCustomValidity("Escreva seu nome para preparar a preferência.");
    input.reportValidity();
    return;
  }
  input.setCustomValidity("");
  confirmed.value = true;
  nextTick(() => booking.value.querySelector(".confirmation-title")?.focus());
}
const downloadHref = computed(() => {
  const text = `AVELINE — ATELIER DE BELEZA\n\nPreferência de atendimento\nNome: ${name.value.trim()}\nIntenção: ${intention.value}\nServiço: ${bookingService.value}\nData: ${date.value ? new Date(date.value + "T12:00:00").toLocaleDateString("pt-BR") : ""}\nPeríodo: ${period.value}\n\nProjeto conceitual. Nenhuma reserva foi feita.\n`;
  return `data:text/plain;charset=utf-8,${encodeURIComponent(text)}`;
});
function closeMenu() {
  menuOpen.value = false;
}
function handleBackdrop(event, dialog) {
  if (event.target === dialog) closeDialog(dialog);
}
function chooseService(index) {
  selectedService.value = index;
  bookingService.value = services[index].name;
}
</script>
<template>
  <header class="opening-header">
    <div class="content-shell opening-bar">
      <button
        ref="menuButton"
        class="opening-menu-toggle"
        :aria-expanded="menuOpen"
        aria-controls="opening-navigation"
        @click="toggleMenu"
      >
        {{ menuOpen ? "Fechar menu" : "Explorar" }}
      </button>
      <a
        href="#inicio"
        class="opening-brand"
        aria-label="Aveline, início"
        @click="closeMenu"
        >AVELINE<span>ATELIER DE BELEZA</span></a
      >
      <button class="opening-book" @click="openBooking()">Sua visita</button>
    </div>
    <nav
      ref="openingNav"
      v-show="menuOpen"
      id="opening-navigation"
      class="content-shell opening-nav"
      aria-label="Navegação principal"
      @keydown.esc.prevent="dismissMenu"
    >
      <p class="eyebrow">CONHEÇA O ATELIER</p>
      <a href="#conversa" @click="closeMenu">Sua primeira conversa</a>
      <a href="#servicos" @click="closeMenu">Cuidados do atelier</a>
      <a href="#caderno" @click="closeMenu">Caderno de cuidados</a>
      <a href="#visita" @click="closeMenu">Planejar sua visita</a>
    </nav>
  </header>
  <main>
    <section id="inicio" class="campaign-hero" aria-labelledby="hero-title">
      <img
        class="campaign-image"
        src="/images/campaign-burgundy-hq.webp"
        alt="Editorial ilustrativo de cabelo castanho em ondas sobre seda vinho"
        fetchpriority="high"
      />
      <div class="content-shell campaign-content">
        <div class="campaign-copy">
          <p class="eyebrow">UM OLHAR INDIVIDUAL</p>
          <h1 id="hero-title">Corte, cor<br />&amp; cuidado</h1>
          <p class="campaign-description">
            Um cuidado pensado para a textura dos seus fios, seu estilo e a sua
            rotina. Tudo começa com uma conversa.
          </p>
          <a href="#conversa" class="button button-blush"
            >Escolher meu cuidado</a
          >
        </div>
      </div>
      <div class="content-shell campaign-caption">
        <span>AVELINE · BELEZA &amp; PRESENÇA</span
        ><a href="#caderno">Conheça o caderno de cuidados</a>
      </div>
    </section>
    <section
      id="conversa"
      class="consultation-scene"
      aria-labelledby="conversation-title"
    >
      <div class="content-shell consultation-layout">
        <div class="consultation-copy">
          <p class="eyebrow">ANTES DO PRIMEIRO ENCONTRO</p>
          <h2 id="conversation-title">O que você<br />quer mudar?</h2>
          <p class="consultation-intro">
            A referência é sua. O cuidado é pensado a partir dela.
          </p>
          <fieldset class="intention-picker">
            <legend>Seu ponto de partida</legend>
            <label v-for="item in intentions" :key="item.title"
              ><input
                type="radio"
                v-model="intention"
                name="intention"
                :value="item.title"
              /><span>{{ item.title }}</span></label
            >
          </fieldset>
          <p class="intention-description" aria-live="polite">
            {{ intentionDetail.text }}
          </p>
          <button class="button button-blush" @click="prepareIntention">
            Conhecer o cuidado indicado
          </button>
        </div>
        <figure class="consultation-photo">
          <img
            src="/images/consultation-cutout.webp"
            alt="Inspiração editorial de corte curto castanho"
            loading="lazy"
          />
        </figure>
      </div>
    </section>
    <div class="atelier-world">
      <section
        id="atelier"
        class="atelier-portrait content-shell"
        aria-labelledby="atelier-title"
      >
        <div class="portrait-heading">
          <p class="eyebrow">O ATELIER</p>
          <h2 id="atelier-title">AVELINE</h2>
          <span class="signature">atelier de beleza</span>
          <p>Seu cabelo tem história.<br />O cuidado começa pela escuta.</p>
          <a class="button button-blush" href="#servicos"
            >Encontre seu cuidado</a
          >
        </div>
        <img
          class="atelier-cutout"
          src="/images/atelier-portrait-hq.webp"
          alt="Retrato editorial ilustrativo de uma mulher de cabelos castanhos e blazer marfim"
          loading="lazy"
        />
        <div class="portrait-note">
          <p>
            Corte, cor e textura, pensados para quem você é. Uma conversa sobre
            suas referências e a rotina fora do espelho. Escolha um cuidado
            abaixo e prepare seu ponto de partida.
          </p>
        </div>
      </section>
      <section
        id="servicos"
        class="care-salon"
        aria-labelledby="services-title"
      >
        <div class="care-paper content-shell">
          <div class="care-paper-heading">
            <p class="eyebrow">MENU DE BELEZA</p>
            <h2 id="services-title">O cuidado, em detalhe</h2>
            <p>
              Escolha o que você tem em mente. Os detalhes são definidos em uma
              avaliação individual.
            </p>
          </div>
          <div
            class="care-options"
            role="tablist"
            aria-label="Cuidados do atelier"
          >
            <button
              v-for="(service, index) in services"
              :key="service.name"
              :id="`service-tab-${index}`"
              role="tab"
              :aria-label="service.name"
              :aria-selected="selectedService === index"
              :tabindex="selectedService === index ? 0 : -1"
              aria-controls="service-panel"
              @click="chooseService(index)"
              @keydown.right.prevent="
                chooseService((index + 1) % services.length);
                $event.target.parentElement.children[selectedService].focus();
              "
              @keydown.left.prevent="
                chooseService((index + services.length - 1) % services.length);
                $event.target.parentElement.children[selectedService].focus();
              "
            >
              <span>{{ service.name }}</span
              ><small>{{ service.hint }}</small>
            </button>
          </div>
          <div
            id="service-panel"
            class="selected-care"
            role="tabpanel"
            :aria-labelledby="`service-tab-${selectedService}`"
          >
            <div>
              <h3>{{ activeService.name }}</h3>
              <p>{{ activeService.description }}</p>
              <p class="selected-detail">{{ activeService.detail }}</p>
            </div>
            <div class="selected-care-action">
              <span>{{ activeService.duration }}</span
              ><button
                class="button button-wine"
                @click="openBooking(activeService.name)"
              >
                Preparar minha visita</button
              ><small>Proposta e valor após avaliação.</small>
            </div>
          </div>
        </div>
        <p class="editorial-note">
          Retrato editorial criado para este projeto conceitual. Não representa
          equipe ou clientes reais.
        </p>
      </section>

      <section
        id="caderno"
        class="care-journal content-shell"
        aria-labelledby="journal-title"
      >
        <div class="journal-intro">
          <p class="eyebrow">CADERNO DE CUIDADOS</p>
          <h2 id="journal-title">Entre uma visita<br />e outra</h2>
          <p class="journal-deck">Pequenos gestos que preservam o resultado e respeitam a textura dos seus fios.</p>
        </div>
        <div class="journal-composition">
          <figure class="journal-photo">
            <img
              src="/images/editorial-curls.webp"
              alt="Inspiração editorial de cabelo cacheado acobreado"
              loading="lazy"
            />
            <figcaption>
              Textura e movimento natural · imagem ilustrativa
            </figcaption>
          </figure>
          <article class="journal-page">
            <div
              class="journal-tabs"
              role="tablist"
              aria-label="Temas do caderno"
            >
              <button
                v-for="(item, index) in journal"
                :key="item.title"
                :id="`journal-tab-${index}`"
                role="tab"
                :aria-selected="journalIndex === index"
                :tabindex="journalIndex === index ? 0 : -1"
                aria-controls="journal-panel"
                @click="journalIndex = index"
                @keydown.right.prevent="
                  journalIndex = (index + 1) % journal.length;
                  $event.target.parentElement.children[journalIndex].focus();
                "
                @keydown.left.prevent="
                  journalIndex = (index + journal.length - 1) % journal.length;
                  $event.target.parentElement.children[journalIndex].focus();
                "
              >
                {{ item.title }}
              </button>
            </div>
            <div
              id="journal-panel"
              role="tabpanel"
              :aria-labelledby="`journal-tab-${journalIndex}`"
            >
              <h3>{{ journal[journalIndex].heading }}</h3>
              <p>{{ journal[journalIndex].text }}</p>
              <ul>
                <li v-for="tip in journal[journalIndex].tips" :key="tip">
                  {{ tip }}
                </li>
              </ul>
              <a href="#visita" class="text-link"
                >Preparar minha próxima visita</a
              >
            </div>
          </article>
        </div>
      </section>
    </div>
    <section id="visita" class="mirror-visit" aria-labelledby="visit-title">
      <div class="content-shell visit-layout">
        <div class="mirror-object">
          <img
            src="/images/atelier-mirror.webp"
            alt="Espelho clássico com moldura dourada e reflexo de um ambiente marfim"
            loading="lazy"
          />
        </div>
        <div class="visit-content">
          <p class="eyebrow">UM TEMPO PARA VOCÊ</p>
          <h2 id="visit-title">Sua visita<br />ao atelier</h2>
          <p class="visit-intro">
            Escolha um cuidado, uma data e o período que combina com seu dia.
          </p>
          <form
            class="visit-form"
            @submit.prevent="openBooking(bookingService)"
          >
            <label for="visit-name"
              >Seu nome<input
                id="visit-name"
                v-model="name"
                required
                maxlength="80"
                autocomplete="given-name"
                placeholder="Como podemos chamar você?"
            /></label>
            <fieldset>
              <legend>Qual cuidado?</legend>
              <div class="visit-choices">
                <label v-for="service in services" :key="service.name"
                  ><input
                    v-model="bookingService"
                    name="visit-service"
                    type="radio"
                    :value="service.name"
                  /><span>{{ service.name }}</span></label
                >
              </div>
            </fieldset>
            <div class="visit-date">
              <label for="visit-date"
                >Data de preferência<input
                  id="visit-date"
                  v-model="date"
                  type="date"
                  :min="today"
                  required
              /></label>
              <fieldset>
                <legend>Período</legend>
                <div class="visit-choices">
                  <label v-for="option in ['Manhã', 'Tarde']" :key="option"
                    ><input
                      v-model="period"
                      type="radio"
                      name="visit-period"
                      :value="option"
                    /><span>{{ option }}</span></label
                  >
                </div>
              </fieldset>
            </div>
            <button type="submit" class="button button-blush">
              Revisar minha preferência
            </button>
            <p class="visit-note">
              Projeto conceitual. A preferência não reserva um horário e seus
              dados não são enviados.
            </p>
          </form>
        </div>
      </div>
    </section>
  </main>
  <footer class="site-footer">
    <div class="content-shell footer-layout">
      <a class="wordmark" href="#inicio">AVELINE</a>
      <p>Atelier de beleza · Projeto conceitual por Giselly Pereira</p>
      <a href="#servicos">Cuidados</a><a href="#visita">Sua visita</a>
    </div>
  </footer>
  <dialog
    ref="booking"
    class="booking-dialog"
    data-lenis-prevent
    aria-labelledby="booking-title"
    @close="afterClose"
    @click="handleBackdrop($event, booking)"
  >
    <div class="dialog-inner">
      <button
        class="dialog-close"
        aria-label="Fechar preferência de horário"
        @click="closeDialog(booking)"
      >
        ×
      </button>
      <template v-if="!confirmed"
        ><p class="eyebrow">SUA VISITA COMEÇA AQUI</p>
        <h2 id="booking-title">Sua visita ao atelier</h2>
        <p class="booking-intro">
          Prepare sua preferência de atendimento. Este site é conceitual e não
          realiza reservas.
        </p>
        <form @submit.prevent="submitPreference">
          <label class="field-label" for="guest-name"
            >Como podemos chamar você?</label
          ><input
            id="guest-name"
            v-model="name"
            @input="$event.target.setCustomValidity('')"
            required
            maxlength="80"
            autocomplete="given-name"
            placeholder="Seu nome"
          />
          <fieldset>
            <legend>Qual cuidado você tem em mente?</legend>
            <div class="choice-list">
              <label v-for="service in services" :key="service.name"
                ><input
                  v-model="bookingService"
                  type="radio"
                  name="service"
                  :value="service.name"
                /><span>{{ service.name }}</span></label
              >
            </div>
          </fieldset>
          <label class="field-label" for="date">Sua data de preferência</label
          ><input id="date" v-model="date" required type="date" :min="today" />
          <fieldset>
            <legend>Em qual período?</legend>
            <div class="choice-list">
              <label v-for="option in ['Manhã', 'Tarde']" :key="option"
                ><input
                  v-model="period"
                  type="radio"
                  name="period"
                  :value="option"
                /><span>{{ option }}</span></label
              >
            </div>
          </fieldset>
          <button class="button button-wine form-submit" type="submit">
            Preparar minha preferência
          </button>
          <p class="form-note">
            Seus dados ficam apenas nesta página e não são enviados.
          </p>
        </form>
      </template>
      <div v-else class="confirmation">
        <p class="eyebrow">PRONTO PARA A CONVERSA</p>
        <h2 id="booking-title" class="confirmation-title" tabindex="-1">
          {{ name.trim().split(" ")[0] }}, sua preferência está pronta
        </h2>
        <dl>
          <div>
            <dt>Seu ponto de partida</dt>
            <dd>{{ intention }}</dd>
          </div>
          <div>
            <dt>Cuidado</dt>
            <dd>{{ bookingService }}</dd>
          </div>
          <div>
            <dt>Preferência</dt>
            <dd>
              {{ new Date(date + "T12:00:00").toLocaleDateString("pt-BR") }} ·
              {{ period }}
            </dd>
          </div>
        </dl>
        <p>
          Nenhum horário foi reservado. Você pode baixar este resumo e usá-lo
          como referência na conversa com seu profissional.
        </p>
        <a
          class="button button-wine"
          :href="downloadHref"
          download="aveline-preferencia.txt"
          >Baixar meu resumo</a
        ><button class="text-link edit-preference" @click="confirmed = false">
          Editar preferência
        </button>
      </div>
    </div>
  </dialog>
</template>
