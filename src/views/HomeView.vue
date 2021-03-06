<template>
  <div>
    <section class="hero  is-hidden-mobile ">
      <div class="hero-body">
        <div class="container">
          <h1 class="title has-text-primary">
            Schluss mit der Zettelwirtschaft
          </h1>
          <h2 class="subtitle">
            Ab sofort führen Sie Ihre Gästeliste online!
          </h2>
        </div>
      </div>
    </section>
    <section class="section">
      <div class="container">
        <div class="notification is-info" v-if="showSignupSuccess">
          {{$t('home.signup_success')}}
        </div>
        <div class="notification is-info" v-if="showPasswortResetSuccess">
          {{$t('home.password_reset_success')}}
        </div>
        <h1 class="title is-1">
          Was ist <IchWarDaTitle/>?
        </h1>
        <div class="columns">
          <div class="column">
            <h3 class="title is-3">
              Für Besucher
            </h3>
            <div class="content is-medium">
              Auf <IchWarDaTitle /> können Sie Ihre Kontaktdaten bei einem Besuch im Restaurant, in der Bar oder
              auch in einem Club ganz einfach hinterlegen. Sie müssen nur den ausgehängten QR Code scannen, Ihre
              Kontaktdaten eingeben und abschicken. Schon sind Ihre Daten erfasst.
            </div>
            <div class="content is-medium">
              Sie müssen dafür kein Konto bei uns anlegen und nach 14 Tagen werden Ihre Daten automatisch gelöscht.
              Sollte es im besuchten Betrieb zu einem COVID-19 Fall kommen, dann kann der Betreiber die Kontaktdaten der betroffnen
              Gäste exportieren und an die Contact Tracer weitergeben.
            </div>
          </div>
          <div class="column">
            <h3 class="title is-3">
              Für Besitzer
            </h3>
            <div class="content is-medium">
              Mit <IchWarDaTitle/> verwalten Sie ab sofort Ihre
              <span class="has-text-weight-semibold has-text-primary">Gästeliste online</span>.
              Nachdem Sie Ihr Betrieb aufgeschaltet haben können Ihre Kunden den
              <span class="has-text-weight-semibold has-text-primary">Besuch</span>
              in Ihrem Betrieb <span class="has-text-weight-semibold has-text-primary">selbstständig registrieren</span>.
              Dafür brauchen sie nur ein Smartphone mit einem Web-Browser mit Internetzugriff.
            </div>
            <div class="content is-medium">
              Natürlichen können Sie die Gästeliste jederzeit online einsehen und bei Bedarf exportieren.
              Die Daten werden auf unserem Server (Serverstandort in der EU) gespeichert und
              <span class="has-text-weight-semibold has-text-primary">nach 14 Tagen automatisch gelöscht</span>.
            </div>
            <div class="content is-medium">
              Neugierig geworden? Dann <router-link to="/demo">probieren Sie unsere Demo</router-link> oder melden
              Sie sich gratis für ein <router-link to="/signup">Konto</router-link> an.
            </div>
          </div>
        </div>

        <div class="columns spacetop">
          <div class="column has-text-centered">
            <p>
              <span class="icon has-text-info">
                <i class="fas fa-2x fa-dice-one"></i>
              </span>
            </p>
            <p class="content is-medium">
              <i class="fas fa-user-edit"></i>
              <router-link to="/signup">
                Konto erstellen
              </router-link>
            </p>

            <p>
              <span class="icon has-text-info">
                <i class="fas fa-2x fa-dice-two"></i>
              </span>
            </p>
            <p class="content is-medium">
              <i class="fas fa-home"></i>
              Betrieb mit Namen und Adresse erfassen
            </p>

            <p>
              <span class="icon has-text-info">
                <i class="fas fa-2x fa-dice-three"></i>
              </span>
            </p>
            <p class="content is-medium">
              <i class="fas fa-qrcode"></i>
              QR-Code ausdrucken und am Eingang (oder am Tisch, an der Wand oder wo auch immer die Kunden ihn sehen koennen) aufhaengen.
            </p>

            <p>
              <span class="icon has-text-info">
                <i class="fas fa-2x fa-dice-d6 fa-spin"></i>
              </span>
            </p>
            <p>
              <i class="fas fa-mobile-alt"></i>
              Nun können sich Ihre Kunden durch Scannen des QR Codes selbstständig registrieren.
            </p>
          </div>
          <div class="column">
            <Login />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script lang="ts">
import {Vue} from 'vue-property-decorator';
import Component from 'vue-class-component';
import Login from '@/components/login/Login.vue';
import IchWarDaTitle from '@/components/IchWarDaTitle.vue';

@Component({
      components: {
        IchWarDaTitle,
          Login
      }
  })
  export default class HomeView extends Vue {
    private showSignupSuccess: boolean = false;
    private showConfirmSuccess: boolean = false;
    private showPasswortResetSuccess: boolean = false;

    public mounted() {
      this.$store.dispatch('account/resetUser');
      console.log(this.$route.query);
      if (this.$route.query.signup === "true") {
        this.showSignupSuccess = true;
      }
      if (this.$route.query.confirm === "true") {
        this.showConfirmSuccess = true;
      }
      if (this.$route.query.resetPassword === "true") {
        this.showPasswortResetSuccess = true;
      }
    }
  }


  //
</script>

<style scoped lang="scss">
  @import './../../node_modules/bulma/sass/utilities/_all';

  .spacetop {
    margin-top: 4em;
  }

  .column {
    padding: 2em;
  }

  .column p .icon {
    margin-bottom: 1.5em;
  }
</style>
